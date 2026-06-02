# Guia de Setup - Corptec

## Pré-requisitos

- Node.js 18+ ([Baixar](https://nodejs.org/))
- PostgreSQL 14+ ([Baixar](https://www.postgresql.org/))
- Git
- npm ou yarn

## Setup Local

### 1. Clonar Repositório

```bash
git clone https://github.com/ROBURO-lab/corptec.git
cd corptec
```

### 2. Instalar Dependências

```bash
npm install
# ou
yarn install
```

### 3. Configurar Variáveis de Ambiente

```bash
cp .env.example .env.local
```

Edite `.env.local` com suas credenciais:

```env
# Database
DATABASE_URL=postgresql://user:password@localhost:5432/corptec
REDIS_URL=redis://localhost:6379

# Firebase
NEXT_PUBLIC_FIREBASE_API_KEY=your_key
NEXT_PUBLIC_FIREBASE_AUTH_DOMAIN=your_domain
NEXT_PUBLIC_FIREBASE_PROJECT_ID=your_project

# Stripe
NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY=pk_test_...
STRIPE_SECRET_KEY=sk_test_...

# AWS S3
AWS_ACCESS_KEY_ID=your_key
AWS_SECRET_ACCESS_KEY=your_secret
AWS_S3_BUCKET=corptec-images
AWS_REGION=us-east-1
```

### 4. Setup com Docker (Recomendado)

```bash
# Inicia PostgreSQL e Redis
docker-compose up -d

# Cria banco de dados
npm run db:migrate

# Seed com dados de exemplo
npm run db:seed
```

### 5. Setup Manual (Sem Docker)

#### PostgreSQL
```bash
# Criar banco de dados
createdb corptec

# Executar migrations
npm run db:migrate -w packages/api

# Seed com dados
npm run db:seed -w packages/api
```

#### Redis
```bash
# Iniciar Redis (macOS com brew)
brew services start redis

# Ou manualmente
redis-server
```

## Desenvolvimento

### Iniciar Todos os Servidores

```bash
npm run dev

# Acessa:
# - Web: http://localhost:3000
# - API: http://localhost:3001
# - Mobile: http://localhost:19000 (Expo)
```

### Iniciar Serviço Específico

```bash
# Web
npm run dev -w apps/web

# API
npm run dev -w packages/api

# Mobile
npm run dev -w apps/mobile

# Desktop
npm run dev -w apps/desktop
```

## Build

### Build Todos

```bash
npm run build
```

### Build Específico

```bash
# Web
npm run build -w apps/web

# API
npm run build -w packages/api
```

## Testes

```bash
# Rodar todos os testes
npm test

# Rodar testes específicos
npm test -w packages/api

# Com coverage
npm test -- --coverage
```

## Lint e Format

```bash
# Lint
npm run lint

# Format com Prettier
npm run format

# Fix automático
npm run lint -- --fix
```

## Troubleshooting

### Erro: "EADDRINUSE: address already in use :::3000"
```bash
# Matar processo na porta 3000
lsof -ti:3000 | xargs kill -9
```

### Erro: "PostgreSQL connection refused"
```bash
# Verificar se PostgreSQL está rodando
pg_isready

# Ou iniciar com Docker
docker-compose up -d postgres
```

### Erro: "Redis connection refused"
```bash
# Verificar se Redis está rodando
redis-cli ping

# Ou iniciar com Docker
docker-compose up -d redis
```

### Erro: "NODE_ENV not set"
```bash
# Linux/macOS
export NODE_ENV=development

# Windows
set NODE_ENV=development
```

## Próximos Passos

1. ✅ Setup concluído
2. 📚 Leia [ARCHITECTURE.md](./ARCHITECTURE.md)
3. 📖 Leia [ROADMAP.md](./ROADMAP.md)
4. 💻 Comece a desenvolver!

## Recursos Úteis

- [Node.js Docs](https://nodejs.org/docs/)
- [Next.js Docs](https://nextjs.org/docs)
- [Express Docs](https://expressjs.com/pt-br/)
- [PostgreSQL Docs](https://www.postgresql.org/docs/)
- [React Native Docs](https://reactnative.dev/docs/getting-started)
