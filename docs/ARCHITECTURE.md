# Arquitetura Corptec

## Visão Geral

```
┌─────────────────────────────────────────────────────────┐
│                    Clientes/Usuários                    │
└────────────┬──────────────────────────┬─────────────────┘
             │                          │
    ┌────────▼────────┐      ┌──────────▼──────────┐
    │   Web App       │      │   Mobile App        │
    │  (Next.js)      │      │  (React Native)     │
    │                 │      │                     │
    │  + Desktop      │      │  + Expo             │
    │  (Electron)     │      │                     │
    └────────┬────────┘      └──────────┬──────────┘
             │                          │
             └──────────────┬───────────┘
                            │
                    ┌───────▼────────┐
                    │   API Gateway  │
                    │  (Express)     │
                    └───────┬────────┘
                            │
        ┌───────────────────┼────────────────────┐
        │                   │                    │
    ┌───▼──┐         ┌──────▼──────┐      ┌─────▼──────┐
    │Auth  │         │  Database   │      │   Cache    │
    │      │         │ PostgreSQL  │      │   Redis    │
    │      │         │             │      │            │
    └──────┘         └─────────────┘      └────────────┘
        │                   │
    ┌───▼──┐         ┌──────▼──────┐
    │      │         │             │
    │      │         │  External   │
    │      │         │  Services   │
    └──────┘         └─────────────┘
                      ├─ Stripe
                      ├─ AWS S3
                      ├─ SendGrid
                      └─ Firebase
```

## Componentes Principais

### 1. Frontend (Cliente)
- **Web**: Next.js 14 (React, TypeScript)
  - Server-side rendering
  - Static generation
  - API routes
  - Otimizado para SEO

- **Mobile**: React Native (Expo)
  - Código compartilhado
  - iOS e Android
  - Performance nativa

- **Desktop**: Electron
  - Windows, macOS, Linux
  - Mesmo código React
  - Sistema de arquivo local

### 2. Backend (API)
- **Framework**: Express.js
- **Banco de Dados**: PostgreSQL
- **Cache**: Redis
- **Autenticação**: JWT + Firebase Auth
- **Pagamentos**: Stripe API

### 3. Serviços Externos
- **Autenticação**: Firebase Authentication
- **Pagamentos**: Stripe
- **Storage**: AWS S3
- **Email**: SendGrid
- **Analytics**: Mixpanel (futuro)

## Fluxo de Dados

### 1. Autenticação
```
Usuário → App → Firebase Auth → JWT Token → API
                                  ↓
                            Protected Routes
```

### 2. Visualização de Produtos
```
Usuário → App → GET /api/products → PostgreSQL
              ← Cached by Redis   ← JSON Response
```

### 3. Pedido
```
Usuário → App → POST /api/orders → Database
                                      ↓
                            → Validação
                            → Cálculo
                            → Notificação
                            → Response
```

### 4. Pagamento
```
Usuário → Stripe Checkout → Webhook → API → Database
           (Seguro)                    ↓
                                  Email Confirm
```

## Banco de Dados

### Tabelas Principais

```sql
-- Usuários/Artesãos
artisans (id, email, name, bio, avatar_url, created_at)

-- Produtos
products (id, artisan_id, name, description, price, 
          images, stock, created_at)

-- Pedidos
orders (id, customer_id, artisan_id, total, status, 
        created_at)

-- Itens do Pedido
order_items (id, order_id, product_id, quantity, price)

-- Avaliações
reviews (id, order_id, customer_id, artisan_id, 
         rating, comment, created_at)

-- Pagamentos
payments (id, order_id, amount, status, stripe_id, 
          created_at)
```

## Segurança

- ✅ HTTPS/TLS
- ✅ JWT Authentication
- ✅ CORS Configurado
- ✅ Rate Limiting
- ✅ SQL Injection Prevention (ORM)
- ✅ XSS Protection
- ✅ CSRF Protection
- ✅ Env Variables para Secrets

## Escalabilidade

- **Cache**: Redis para frequent queries
- **CDN**: Cloudflare para assets estáticos
- **Database**: Connection pooling
- **API**: Load balancing com Nginx
- **Storage**: S3 para imagens

## Deployment

### Development
```
docker-compose up
```

### Production
- **Web**: Vercel
- **API**: AWS ECS / EC2
- **Database**: AWS RDS
- **Storage**: AWS S3
- **Cache**: AWS ElastiCache

## Monitoramento

- **Logs**: CloudWatch / ELK Stack
- **Metrics**: Prometheus
- **APM**: New Relic / DataDog
- **Errors**: Sentry
