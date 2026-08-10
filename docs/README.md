# Atlas Commerce Roadmap

Este documento apresenta a visão evolutiva do Atlas Commerce, organizando o desenvolvimento do projeto em missões, sprints e grandes entregas.

---

# Pré-Projeto

Etapa responsável pela definição da fundação técnica, arquitetura inicial e infraestrutura do projeto.

- ✓ Missão 000 — Fundação do Projeto
- ✓ Missão 001 — Arquitetura Inicial
- ✓ Missão 002 — Definições Técnicas
- ✓ Missão 003 — PostgreSQL Foundation

---

# Sprint 001 — Core Domain

Objetivo: construir a fundação dos principais domínios do Atlas Commerce.

- □ Missão 004 — Category
- □ Missão 005 — Product
- □ Missão 006 — Inventory
- □ Missão 007 — Order
- □ Missão 008 — Payment
- □ Missão 009 — Cart
- □ Missão 010 — Checkout

---

# Sprint 002 — Product & Inventory

Objetivo: consolidar o gerenciamento de produtos e estoque.

- □ Product
- □ Inventory
- □ Upload

---

# Sprint 003 — Commerce Flow

Objetivo: implementar o fluxo principal de compra.

- □ Cart
- □ Order
- □ Checkout

---

# Sprint 004 — User Management

Objetivo: implementar o gerenciamento de usuários.

- □ User
- □ Profile
- □ Address

---

# Sprint 005 — Authentication & Security

Objetivo: implementar autenticação, autorização e segurança da plataforma.

- □ Authentication
- □ Authorization
- □ JWT
- □ Security

---

# Sprint 006 — Administration

Objetivo: construir os recursos administrativos da plataforma.

- □ Dashboard
- □ Reports
- □ Metrics

---

# Sprint 007 — Production

Objetivo: preparar o Atlas Commerce para execução em ambiente de produção.

- □ Production Environment
- □ CI/CD
- □ Deployment
- □ Monitoring

---

# Visão Geral

```text
Pré-Projeto
    │
    ├── Missão 000
    ├── Missão 001
    ├── Missão 002
    └── Missão 003
             │
             ▼
      Sprint 001
             │
             ├── Missão 004 — Category
             ├── Missão 005 — Product
             ├── Missão 006 — Inventory
             ├── Missão 007 — Order
             ├── Missão 008 — Payment
             ├── Missão 009 — Cart
             └── Missão 010 — Checkout
             │
             ▼
      Sprint 002
             │
             ├── Product & Inventory
             └── Upload
             │
             ▼
      Sprint 003
             │
             ├── Cart
             ├── Order
             └── Checkout
             │
             ▼
      Sprint 004
             │
             └── User Management
             │
             ▼
      Sprint 005
             │
             └── Authentication & Security
             │
             ▼
      Sprint 006
             │
             └── Administration
             │
             ▼
      Sprint 007
             │
             └── Production