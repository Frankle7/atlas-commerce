# Milestone 01 — Foundation & Category Module

---

# Objetivo

Definir oficialmente o primeiro grande marco do desenvolvimento do Atlas Commerce.

O Milestone 01 representa a conclusão da fundação técnica do projeto e a implementação completa do primeiro domínio de negócio: **Category**.

Ao finalizar este marco, o projeto estará preparado para que todos os demais módulos sejam desenvolvidos utilizando exatamente a mesma arquitetura.

---

# Contexto

Todo software complexo precisa de uma fundação sólida.

Antes de implementar dezenas de funcionalidades é necessário validar toda a arquitetura da aplicação.

Por esse motivo o primeiro Milestone concentra esforços em:

- estrutura do projeto;
- arquitetura;
- padrões;
- documentação;
- primeiro módulo completo.

A partir dele todos os próximos módulos serão implementados reutilizando a mesma base.

---

# Visão Geral

```
Pré-Projeto

↓

Missão 001
Planejamento

↓

Missão 002
Arquitetura

↓

Missão 003
Setup

↓

Sprint 001

↓

Missão 004
Category Domain

↓

Missão 005
Category Service

↓

Missão 006
Category API

↓

Missão 007
Validation

↓

Missão 008
Swagger

↓

Missão 009
Tests

↓

Missão 010
Code Review

↓

Milestone 01 Finalizado
```

---

# Objetivos do Milestone

Este marco possui seis grandes objetivos.

## Objetivo 01

Validar toda arquitetura do Atlas Commerce.

---

## Objetivo 02

Criar o primeiro módulo completo.

(Category)

---

## Objetivo 03

Estabelecer padrões de desenvolvimento.

---

## Objetivo 04

Construir toda documentação técnica.

---

## Objetivo 05

Validar fluxo Git.

- Feature Branch
- Sprint
- Main
- Pull Request
- Code Review

---

## Objetivo 06

Preparar a base para os próximos módulos.

---

# Escopo

Este Milestone contempla apenas o domínio Category.

Não fazem parte deste marco:

- Product
- Order
- Payment
- Cart
- Inventory

Esses módulos pertencem aos próximos Milestones.

---

# Estrutura das Missões

## Missão 004 — Category Domain

### Objetivo

Implementar a camada de domínio.

### Entregáveis

- Entity
- Repository
- Migration
- Specification
- Validator
- ADR-006

### Critérios de Aceite

✔ Entity criada.

✔ Migration funcionando.

✔ Repository implementado.

✔ Banco sincronizado.

---

## Missão 005 — Category Service

### Objetivo

Implementar toda regra de negócio.

### Entregáveis

- CategoryService
- DTOs
- Mapper
- Validações

### Critérios de Aceite

✔ CRUD funcionando.

✔ Regras implementadas.

✔ Service desacoplada.

---

## Missão 006 — Category API

### Objetivo

Disponibilizar endpoints REST.

### Entregáveis

```
GET /categories

GET /categories/{id}

POST /categories

PUT /categories/{id}

DELETE /categories/{id}
```

### Critérios de Aceite

✔ Endpoints funcionando.

✔ DTOs utilizados.

✔ HTTP Status corretos.

---

## Missão 007 — Validation & Exception

### Objetivo

Padronizar validações.

### Entregáveis

- Validators
- Exception Handler
- Error Pattern

### Critérios de Aceite

✔ Erros padronizados.

✔ Validações centralizadas.

---

## Missão 008 — Swagger

### Objetivo

Gerar documentação automática.

### Entregáveis

- OpenAPI
- Swagger UI
- Exemplos

### Critérios de Aceite

✔ Todos endpoints documentados.

---

## Missão 009 — Testes

### Objetivo

Garantir qualidade.

### Entregáveis

- Unit Tests
- Integration Tests

### Critérios de Aceite

✔ Cobertura mínima definida.

✔ Build aprovado.

---

## Missão 010 — Code Review

### Objetivo

Finalizar a Sprint.

### Entregáveis

- Refatorações
- Melhorias
- Revisão

### Critérios de Aceite

✔ Código aprovado.

✔ ADR atualizado quando necessário.

✔ Documentação revisada.

---

# Estrutura Git

Durante este Milestone o fluxo oficial será:

```
main

↓

sprint-001

↓

feature/mission-004-category

↓

feature/mission-005-category-service

↓

feature/mission-006-category-api

↓

feature/mission-007-validation

↓

feature/mission-008-swagger

↓

feature/mission-009-tests

↓

feature/mission-010-review
```

Cada missão possui sua própria Feature Branch.

---

# Organização dos Commits

Cada Feature deve conter commits pequenos e semânticos.

Exemplo:

```
feat(category): create entity

feat(category): create repository

feat(category): add migration

docs(adr): add category architecture

test(category): add repository tests
```

Nunca misturar documentação e implementação no mesmo commit.

---

# Documentação Produzida

Ao final deste Milestone estarão concluídos:

```
API

Architecture

Standards

Deployment

Roadmap

ADR

Mission Docs

Onboarding
```

Toda documentação acompanha a evolução do código.

---

# Critérios Gerais de Aceite

O Milestone será considerado concluído quando:

- todas as missões estiverem finalizadas;
- todas as ADRs estiverem atualizadas;
- documentação revisada;
- testes aprovados;
- Swagger funcionando;
- banco versionado;
- arquitetura preservada;
- Code Review concluído.

---

# Fora do Escopo

Este Milestone não contempla:

- autenticação JWT;
- produtos;
- pedidos;
- pagamentos;
- carrinho;
- notificações;
- CI/CD completo.

Esses itens pertencem aos próximos marcos.

---

# Resultado Esperado

Ao concluir o Milestone 01 o Atlas Commerce possuirá:

- arquitetura consolidada;
- primeiro módulo completo;
- documentação técnica estruturada;
- padrões definidos;
- fluxo Git validado;
- base pronta para expansão.

---

# Relação com Outros Documentos

Este documento complementa:

- ROADMAP.md
- MISSION-001.md
- MISSION-002.md
- MISSION-003.md
- ADR-000
- ADR-006

---

# Benefícios

A conclusão deste Milestone proporciona:

- fundação técnica estável;
- padronização do desenvolvimento;
- facilidade para novos colaboradores;
- alta escalabilidade;
- reutilização da arquitetura;
- menor custo de manutenção.

---

# Referências

- Scrum Guide
- Domain Driven Design
- Clean Architecture
- Spring Boot Documentation
- REST API Design

---

# Próximo Capítulo

roadmap/MILESTONE-02.md