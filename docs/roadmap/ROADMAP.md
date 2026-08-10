# Roadmap

---

# Objetivo

Definir a visão estratégica e a evolução planejada do Atlas Commerce.

Este documento apresenta o caminho completo do projeto, desde sua fundação técnica até a construção de uma plataforma de e-commerce escalável, modular e preparada para crescimento contínuo.

Ao concluir este capítulo, o desenvolvedor compreenderá:

- onde o projeto está;
- para onde ele irá;
- quais funcionalidades serão construídas;
- como as entregas estão organizadas;
- qual a estratégia de evolução do produto.

---

# Contexto

Grandes sistemas não são construídos de uma única vez.

Eles evoluem em pequenas entregas.

Cada Sprint adiciona novas capacidades ao sistema.

Cada Missão resolve um problema específico.

Cada ADR registra uma decisão importante.

O Roadmap conecta todas essas peças.

---

# Filosofia do Projeto

O Atlas Commerce é construído seguindo cinco princípios fundamentais.

### 1. Evolução incremental

Pequenas entregas contínuas.

---

### 2. Arquitetura sustentável

O projeto deve continuar organizado mesmo após anos de evolução.

---

### 3. Qualidade antes de velocidade

Toda funcionalidade deve possuir:

- documentação;
- testes;
- revisão;
- padronização.

---

### 4. Documentação como conhecimento

A documentação não explica apenas "o que fazer".

Ela ensina:

- arquitetura;
- boas práticas;
- decisões;
- padrões.

---

### 5. Escalabilidade

O Atlas deve estar preparado para:

- mais módulos;
- mais desenvolvedores;
- mais clientes;
- mais integrações.

---

# Visão Geral do Projeto

```
Atlas Commerce

│
├── Backend
│
├── Frontend
│
├── Mobile
│
├── Infraestrutura
│
├── Banco de Dados
│
├── APIs
│
├── Documentação
│
└── DevOps
```

Todos os componentes evoluem em paralelo.

---

# Estrutura do Planejamento

O projeto é dividido em:

```
Projeto

↓

Milestones

↓

Sprints

↓

Missões

↓

Features

↓

Commits
```

Cada nível possui uma responsabilidade.

---

# Pré-Projeto

Antes do desenvolvimento funcional foi criada a base do sistema.

---

## Missão 001 — Planejamento

Objetivos:

- visão do produto;
- definição dos módulos;
- definição das sprints;
- organização do roadmap.

Entregáveis:

- ROADMAP.md
- milestones
- planejamento técnico.

---

## Missão 002 — Arquitetura

Objetivos:

- definir arquitetura;
- modularização;
- Package by Feature;
- ADRs.

Entregáveis:

- architecture/
- ADRs
- diagramas.

---

## Missão 003 — Setup

Objetivos:

- Spring Boot;
- PostgreSQL;
- Docker;
- Flyway;
- estrutura inicial.

Entregáveis:

- backend;
- docker;
- banco;
- configuração inicial.

---

# Linha do Tempo

```
Missão 001

↓

Missão 002

↓

Missão 003

↓

Sprint 001

↓

Sprint 002

↓

Sprint 003

↓

Release 1.0
```

---

# Sprint 001 — Category Module

Objetivo:

Construir o primeiro módulo completo do sistema.

---

## Missão 004 — Category Domain

Entrega:

- Entity;
- Repository;
- Migration;
- ADR.

---

## Missão 005 — Category Service

Entrega:

- regras de negócio;
- validações;
- service layer.

---

## Missão 006 — Category API

Entrega:

- controllers;
- DTOs;
- endpoints.

---

## Missão 007 — Validation & Exception

Entrega:

- validações;
- tratamento global de erros.

---

## Missão 008 — Swagger

Entrega:

- documentação automática.

---

## Missão 009 — Testes

Entrega:

- testes unitários;
- testes integração.

---

## Missão 010 — Code Review

Entrega:

- revisão;
- melhorias;
- refatorações.

---

# Sprint 002 — Product Module

Objetivo:

Implementar gerenciamento de produtos.

---

Missões previstas:

- Product Entity
- Product Service
- Product API
- Product Validation
- Product Tests

---

# Sprint 003 — Inventory Module

Objetivo:

Controle de estoque.

---

Possíveis entregas:

- movimentação;
- reserva;
- disponibilidade.

---

# Sprint 004 — Cart Module

Objetivo:

Carrinho de compras.

---

Possíveis entregas:

- adicionar item;
- remover item;
- cálculo de total.

---

# Sprint 005 — Order Module

Objetivo:

Processamento de pedidos.

---

Possíveis entregas:

- criação;
- pagamento;
- status.

---

# Sprint 006 — Payment Module

Objetivo:

Integrações financeiras.

---

Possíveis integrações:

- Stripe;
- Mercado Pago;
- Pix.

---

# Sprint 007 — Authentication

Objetivo:

Segurança da aplicação.

---

Entregas:

- JWT;
- autorização;
- permissões.

---

# Sprint 008 — Notification

Objetivo:

Comunicação.

---

Entregas:

- e-mail;
- SMS;
- notificações.

---

# Sprint 009 — Observabilidade

Objetivo:

Monitoramento.

---

Entregas:

- logs;
- métricas;
- tracing.

---

# Sprint 010 — CI/CD Completo

Objetivo:

Automação total.

---

Entregas:

- GitHub Actions;
- deploy;
- pipeline.

---

# Evolução Técnica

```
Monólito Modular

↓

Monólito Escalável

↓

Serviços Independentes

↓

Microsserviços (futuro)
```

A arquitetura atual já prepara essa possibilidade.

---

# Releases

Exemplo:

```
v0.1.0

↓

v0.2.0

↓

v0.3.0

↓

v1.0.0
```

Seguimos Semantic Versioning.

---

# Indicadores de Evolução

A cada Sprint avaliamos:

- cobertura de testes;
- tempo de build;
- qualidade;
- performance;
- documentação.

---

# O que NÃO fazer

Nunca:

- iniciar Sprint sem Missão;
- implementar sem documentação;
- ignorar ADRs;
- misturar módulos.

---

# Boas Práticas

✔ Pequenas entregas.

✔ Commits organizados.

✔ ADRs atualizados.

✔ Testes.

✔ Revisão.

✔ Documentação.

✔ Evolução incremental.

---

# Benefícios

O Roadmap proporciona:

- previsibilidade;
- organização;
- alinhamento;
- escalabilidade;
- rastreabilidade.

---

# Relação com Outros Documentos

- MILESTONE-01.md
- MILESTONE-02.md
- RELEASES.md
- MISSION-001.md
- MISSION-002.md
- MISSION-003.md

---

# Decisão Arquitetural

Relaciona-se com:

- ADR-000 — Arquitetura Geral
- ADR-005 — Package by Feature

---

# Referências

- Agile Manifesto
- Scrum Guide
- Domain Driven Design
- Clean Architecture

---

# Próximo Capítulo

roadmap/MILESTONE-01.md