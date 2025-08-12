# 🚀 DevSignIn - API de Autenticação com NestJS

> **Projeto desenvolvido para fins didáticos** - Aplicação de autenticação completa utilizando NestJS, MongoDB e JWT

## 📚 Sobre o Curso

**Nome do Curso:** NestJS do Zero com TypeORM, Mongoose, Prisma e Swagger  
**Professor:** Jorge Aluizio Alves Souza  
**Plataforma:** Udemy

---

## 🎯 Objetivos de Aprendizado

Este projeto foi desenvolvido com o objetivo de:

- **Conhecer os principais recursos do framework NestJS** para criação de aplicativos com o Node.js
- **Integrar o Mongoose ao NestJS** aplicado com o banco de dados MongoDB
- **Criar API RESTful com autenticação via Token JWT** com MongoDB e Mongoose

---

## 🏗️ Arquitetura da Aplicação

### Tecnologias Utilizadas

- **Backend:** NestJS (Framework Node.js)
- **Banco de Dados:** MongoDB
- **ORM:** Mongoose
- **Autenticação:** JWT (JSON Web Tokens)
- **Validação:** Class-validator e Class-transformer
- **Criptografia:** bcrypt
- **Linguagem:** TypeScript

### Estrutura do Projeto

```
src/
├── auth/                    # Módulo de autenticação
│   ├── auth.module.ts      # Configuração do módulo
│   ├── auth.service.ts     # Serviços de autenticação
│   ├── models/             # Modelos JWT
│   └── strategies/         # Estratégias Passport
├── users/                  # Módulo de usuários
│   ├── dto/               # Data Transfer Objects
│   ├── models/            # Modelos de usuário
│   ├── schemas/           # Schemas Mongoose
│   ├── users.controller.ts # Controlador REST
│   ├── users.service.ts   # Lógica de negócio
│   └── users.module.ts    # Configuração do módulo
├── app.module.ts          # Módulo principal
├── main.ts               # Ponto de entrada
└── ...
```

---

## 🚀 Como Executar Localmente

### Pré-requisitos

- Node.js (versão 18 ou superior)
- MongoDB instalado e rodando
- pnpm (ou npm/yarn)

### Passo a Passo

#### 1. Clone o repositório

```bash
git clone <url-do-repositorio>
cd devsignin
```

#### 2. Instale as dependências

```bash
pnpm install
# ou
npm install
# ou
yarn install
```

#### 3. Configure as variáveis de ambiente

Crie um arquivo `.env` na raiz do projeto:

```env
PORT=3000
MONGODB_URI=mongodb://localhost:27017/devsignin
JWT_SECRET=sua_chave_secreta_aqui
```

#### 4. Inicie o MongoDB

```bash
docker run -d -p 27017:27017 --name mongodb mongo:latest
```

#### 5. Execute a aplicação

**Modo desenvolvimento (com hot-reload):**

```bash
pnpm run start:dev
```

**Modo produção:**

```bash
pnpm run build
pnpm run start:prod
```

#### 6. Acesse a aplicação

A API estará disponível em: `http://localhost:3000`

---

## 📡 Endpoints da API

| Método | Endpoint        | Descrição                | Autenticação |
| ------ | --------------- | ------------------------ | ------------ |
| `POST` | `/users/signup` | Cadastrar novo usuário   | ❌           |
| `POST` | `/users/signin` | Fazer login              | ❌           |
| `GET`  | `/users`        | Listar todos os usuários | ✅ JWT       |

### Detalhes dos Endpoints

#### POST `/users/signup`

Cadastra um novo usuário no sistema.

**Body:**

```json
{
  "name": "João Silva",
  "email": "joao@email.com",
  "password": "123456"
}
```

**Resposta (201):**

```json
{
  "id": "uuid-gerado",
  "name": "João Silva",
  "email": "joao@email.com"
}
```

#### POST `/users/signin`

Autentica um usuário e retorna um token JWT.

**Body:**

```json
{
  "email": "joao@email.com",
  "password": "123456"
}
```

**Resposta (200):**

```json
{
  "name": "João Silva",
  "email": "joao@email.com",
  "jwtToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}
```

#### GET `/users`

Lista todos os usuários cadastrados (requer autenticação).

**Headers:**

```
Authorization: Bearer <jwt-token>
```

**Resposta (200):**

```json
[
  {
    "id": "uuid-1",
    "name": "João Silva",
    "email": "joao@email.com"
  },
  {
    "id": "uuid-2",
    "name": "Maria Santos",
    "email": "maria@email.com"
  }
]
```

---

## 🔐 Funcionalidades de Segurança

### Criptografia de Senhas

- Senhas são criptografadas usando bcrypt com salt de 10 rounds
- Middleware automático do Mongoose para hash de senhas

### Autenticação JWT

- Tokens JWT para autenticação de usuários
- Estratégia Passport JWT implementada
- Guardas de rota para proteção de endpoints

### Validação de Dados

- Validação automática de DTOs usando class-validator
- Sanitização de entrada com class-transformer
- Validação de email e comprimento mínimo de senha

---

## 🧪 Testes

### Executar testes unitários

```bash
pnpm run test
```

### Executar testes em modo watch

```bash
pnpm run test:watch
```

### Executar testes com cobertura

```bash
pnpm run test:cov
```

### Executar testes end-to-end

```bash
pnpm run test:e2e
```

---

## 🛠️ Scripts Disponíveis

| Comando                | Descrição                      |
| ---------------------- | ------------------------------ |
| `pnpm run build`       | Compila o projeto              |
| `pnpm run start`       | Inicia a aplicação             |
| `pnpm run start:dev`   | Inicia em modo desenvolvimento |
| `pnpm run start:debug` | Inicia em modo debug           |
| `pnpm run start:prod`  | Inicia em modo produção        |
| `pnpm run test`        | Executa testes unitários       |
| `pnpm run test:e2e`    | Executa testes end-to-end      |
| `pnpm run lint`        | Executa linting do código      |
| `pnpm run format`      | Formata o código com Prettier  |

---

## 📦 Dependências Principais

### Dependências de Produção

- `@nestjs/common` - Funcionalidades core do NestJS
- `@nestjs/mongoose` - Integração com Mongoose
- `@nestjs/jwt` - Suporte a JWT
- `@nestjs/passport` - Estratégias de autenticação
- `mongoose` - ODM para MongoDB
- `bcrypt` - Criptografia de senhas
- `class-validator` - Validação de dados
- `passport-jwt` - Estratégia JWT para Passport

### Dependências de Desenvolvimento

- `@nestjs/cli` - CLI do NestJS
- `typescript` - Compilador TypeScript
- `jest` - Framework de testes
- `eslint` - Linting de código
- `prettier` - Formatação de código

---

## 🔧 Configuração do Banco de Dados

### MongoDB

- **Porta padrão:** 27017
- **Database:** devsignin
- **Coleção:** users

### Schema do Usuário

```typescript
{
  name: String,      // Nome do usuário (obrigatório)
  email: String,     // Email único (obrigatório)
  password: String   // Senha criptografada (obrigatório)
}
```

---

## 🚨 Tratamento de Erros

A aplicação inclui tratamento robusto de erros:

- **Validação de entrada** com mensagens claras
- **Tratamento de erros de banco** (duplicação de email, etc.)
- **Respostas HTTP apropriadas** para cada tipo de erro
- **Logs estruturados** para debugging

---

## 📈 Próximos Passos

Para expandir esta aplicação, considere:

- [ ] Implementar refresh tokens
- [ ] Adicionar roles e permissões
- [ ] Implementar rate limiting
- [ ] Adicionar logs estruturados
- [ ] Implementar cache com Redis
- [ ] Adicionar documentação Swagger
- [ ] Implementar testes de integração
- [ ] Adicionar CI/CD pipeline

---

## 🤝 Contribuição

Este é um projeto educacional. Para contribuir:

1. Faça um fork do projeto
2. Crie uma branch para sua feature
3. Commit suas mudanças
4. Push para a branch
5. Abra um Pull Request

---

## 📄 Licença

Este projeto é para fins educacionais e não possui licença específica.

---

## 👨‍🏫 Créditos

**Curso:** NestJS do Zero com TypeORM, Mongoose, Prisma e Swagger  
**Professor:** Jorge Aluizio Alves Souza  
**Plataforma:** Udemy

---

## 📞 Suporte

Para dúvidas sobre o projeto ou problemas técnicos, consulte:

- Documentação oficial do NestJS: https://nestjs.com/
- Documentação do Mongoose: https://mongoosejs.com/
- Documentação do MongoDB: https://docs.mongodb.com/

---

**Desenvolvido com ❤️ para fins educacionais**
