# Back-End NodeJs do NLW-07 HEAT - RocketSeat

## Tecnologias utilizadas

- Javascript (Linguagem programação)
- Node Js (Ambiente de Execução Javascript)
- Typescript (Tipagem Javascript)
- REST (Arquitetura)
- Oauth2 (Autenticação)
- JWT - Json Web Token
- Prisma (ORM)
- Socket.IO (Realtime WEB Application)

### Bibliotecas utilizadas

- @prisma/client : client do Prisma ORM
- axios : HTTP client
- cors : habilitar CORS no Express
- dotenv : habilitar .env environment variables
- express : web framework js
- jsonwebtoken : implementador JWT
- socket.io : realtime web application
- prisma (dev) : ORM (Object Relational Mapper)
- ts-node-dev : Compila aplicativo TS e reinicia quando modificado
- typescript : adiciona tipagem para javascript

## Resumo do fluxo de autenticação Oauth

### Front-End

- Solicitação de login : https://github.com/login/oauth/authorize?client_id=id_do_client
- Autorização e Credenciais do github se preciso
- Callback da solicitação do Login : exemplo http://localhost:3000/signin/callback para receber o código para login
- Enviar o código para o back-end: post para http://localhost:4000/authenticate com o código no corpo da requisição (code)
- Recebe um token do back-end para acesso aos recursos

### Back-End

- Recebe código fornecido pelo github do front-end
- Recupera o access_token no github
- Recupera informações do usuário no github
- Verificar se o usuário já existe no banco de dados
  - caso Sim: Gera um token
  - caso Não: Cria novo usuário no banco de dados e gera um token
- Retornar ao front-end um token e as informações do usuário

## Utilização resumida do Prisma

- execução no terminal "yarn prisma init" para inicializar o prima num projeto já criado
- configurar o prisma nos arquivos .env e schema.prisma com o banco de dados utilizado
- criar um modelo (ORM) no arquivo schema.prisma
- depois de criar um modelo executar no terminal "yarn prisma migrate dev" para criar
  o migration.sql, no caso, e para criação da tabela no banco de dados.
- criar um prisma client (ex: /src/prisma/index.ts)
- utilizar o prisma client nos serviços para requisições ao banco de dados.

## Utilização resumida do Socket.IO no app

- criado servidor socket IO com base em um servidor http
- habilitado servidor socket IO (método on()) quando conectado
- quando uma nova mensagem é criada o servidor socket IO emite uma informação de
  "nova_mensagem" que serão recebidas por todos que tiverem escutando "nova_mensagem"
