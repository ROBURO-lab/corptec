# Corptec - Vitrine para Artesãos

Uma plataforma automatizada completa para artesãos exibirem seus produtos, gerenciarem pedidos e receberem pagamentos.

## 🚀 Características Principais

- **Vitrine Online**: Portfólio de produtos com fotos e descrições
- **Carrinho de Compras**: Sistema completo de compras
- **Gestão de Pedidos**: Automação de pedidos e notificações
- **Perfil do Artesão**: Exibição de dados e avaliações
- **Busca e Filtros**: Descoberta fácil de produtos
- **Sistema de Pagamento**: Integração com Stripe
- **Avaliações**: Comentários e ratings de clientes
- **Multi-plataforma**: Web, Mobile (iOS/Android), Desktop

## 📱 Tech Stack

### Frontend
- **Web**: React + Next.js 14 (TypeScript)
- **Mobile**: React Native (Expo)
- **Desktop**: Electron + React

### Backend
- **API**: Node.js + Express
- **Database**: PostgreSQL
- **Cache**: Redis
- **Autenticação**: Firebase Auth
- **Pagamentos**: Stripe API
- **Storage**: AWS S3 (imagens)

### DevOps
- **CI/CD**: GitHub Actions
- **Container**: Docker
- **Hosting**: Vercel (Web), AWS (Backend)

## 📁 Estrutura do Projeto

```
corptec/
├── apps/
│   ├── web/                 # Aplicação Next.js Web
│   ├── mobile/              # React Native (Expo)
│   └── desktop/             # Electron App
├── packages/
│   ├── api/                 # API Node.js + Express
│   ├── shared/              # Código compartilhado (tipos, utils)
│   └── ui/                  # Componentes reutilizáveis
├── infrastructure/          # Docker, K8s configs
├── docs/                    # Documentação
└── .github/workflows/       # CI/CD Workflows
```

## 🛠️ Instalação

### Pré-requisitos
- Node.js 18+
- PostgreSQL 14+
- Git

### Setup Local

```bash
# Clonar repositório
git clone https://github.com/ROBURO-lab/corptec.git
cd corptec

# Instalar dependências (workspace monorepo)
npm install

# Setup de variáveis de ambiente
cp .env.example .env.local

# Rodar migrations do banco
npm run db:migrate

# Iniciar servidores em desenvolvimento
npm run dev
```

## 📚 Documentação

- [Guia de Configuração](./docs/SETUP.md)
- [Arquitetura](./docs/ARCHITECTURE.md)
- [Roadmap](./docs/ROADMAP.md)
- [Contribuição](./CONTRIBUTING.md)

## 📊 Roadmap

- [ ] Fase 1: Autenticação e Perfil do Artesão
- [ ] Fase 2: Catálogo e Galeria de Produtos
- [ ] Fase 3: Carrinho e Sistema de Pedidos
- [ ] Fase 4: Integração Stripe (Pagamentos)
- [ ] Fase 5: App Mobile (React Native)
- [ ] Fase 6: App Desktop (Electron)
- [ ] Fase 7: Analytics e Dashboard
- [ ] Fase 8: Marketing e SEO

## 🤝 Contribuindo

Leia [CONTRIBUTING.md](./CONTRIBUTING.md) para detalhes sobre nosso código de conduta e processo de pull request.

## 📄 Licença

Este projeto está sob a licença MIT.

## 👥 Autores

- ROBURO-lab Team

---

**Status**: Em desenvolvimento 🔄
