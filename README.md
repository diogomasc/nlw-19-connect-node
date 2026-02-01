# NLW Connect Node

Aplicação backend desenvolvida durante o NLW Connect da Rocketseat. Este sistema gerencia inscrições em eventos e um sistema de ranking de indicações, utilizando uma stack focada em performance e experiência do desenvolvedor.

## 🚀 Tecnologias

- **Node.js** & **TypeScript**
- **Fastify** - Framework web rápido e leve
- **Drizzle ORM** - ORM TypeScript para SQL
- **PostgreSQL** - Banco de dados relacional
- **Redis** - Armazenamento de dados em memória para ranking
- **Zod** - Validação de schemas
- **Swagger** - Documentação da API

## 🛠️ Pré-requisitos

- **Node.js** (v20+)
- **Docker** & **Docker Compose**

## 🔧 Instalação e Configuração

1. **Clone o repositório**

   ```bash
   git clone https://github.com/diogomasc/nlw-19-connect-node.git
   cd nlw-connect-node
   ```

2. **Instale as dependências**

   ```bash
   npm install
   ```

3. **Inicie os serviços de banco de dados e redis**

   ```bash
   docker-compose up -d
   ```

4. **Configure as Variáveis de Ambiente**
   Crie um arquivo `.env` na raiz do projeto baseado no exemplo abaixo:

   ```env
   # Server
   PORT=3333

   # Database
   DATABASE_URL="postgresql://docker:docker@localhost:5432/connect"

   # Redis
   REDIS_URL="redis://localhost:6379"

   # URLs
   API_URL="http://localhost:3333"
   WEB_URL="http://localhost:3000"
   ```

5. **Execute as Migrations do Banco de Dados**

   ```bash
   npm run db:migrate
   ```

6. **Inicie o Servidor de Desenvolvimento**

   ```bash
   npm run dev
   ```

   O servidor iniciará em `http://localhost:3333`.

## 📖 Documentação da API

A documentação completa da API está disponível via Swagger UI em:
**http://localhost:3333/docs**

### Rotas Principais

#### Inscrições (Subscriptions)

- **POST** `/subscriptions`
  - Cria uma nova inscrição no evento.
  - Corpo: `{ "name": "Fulano", "email": "fulano@exemplo.com", "referrer": "id-opcional" }`

#### Convites (Invites)

- **GET** `/invites/:subscriberId`
  - Obtém o link de convite para um inscrito específico.

#### Ranking

- **GET** `/ranking`
  - Obtém o ranking global dos principais indicadores.

- **GET** `/subscribers/:subscriberId/ranking/count`
  - Obtém a contagem de convites de um inscrito.

- **GET** `/subscribers/:subscriberId/ranking/clicks`
  - Obtém o número de cliques no link de convite de um inscrito.

- **GET** `/subscribers/:subscriberId/ranking/position`
  - Obtém a posição atual de um inscrito no ranking.

## 📝 Scripts

- `npm run dev`: Inicia o servidor de desenvolvimento em modo watch.
- `npm run build`: Compila a aplicação para produção.
- `npm run start`: Inicia o servidor de produção.
- `npm run db:generate`: Gera migrações SQL a partir do schema do Drizzle.
- `npm run db:migrate`: Aplica as migrações ao banco de dados.
