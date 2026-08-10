# Milestone 02 — Product Module & Catalog Foundation

---

# Objetivo

Definir oficialmente o segundo grande marco do desenvolvimento do Atlas Commerce.

O Milestone 02 é responsável pela construção completa do módulo **Product**, responsável pelo gerenciamento do catálogo de produtos da plataforma.

Ao concluir este marco, o Atlas Commerce possuirá dois domínios totalmente funcionais (Category e Product), estabelecendo a base do catálogo de produtos do sistema.

---

# Contexto

Após validar toda a arquitetura através do módulo Category, o próximo passo é implementar um domínio mais complexo.

O módulo Product introduz novos desafios arquiteturais:

- relacionamento entre entidades;
- regras de negócio mais elaboradas;
- consultas dinâmicas;
- paginação;
- filtros;
- documentação completa;
- testes mais robustos.

Este Milestone também valida se a arquitetura criada no Milestone 01 realmente suporta a evolução contínua do projeto.

---

# Visão Geral

```
Milestone 01
(Fundação)

↓

Category

↓

Milestone 02

↓

Product Domain

↓

Product Service

↓

Product API

↓

Product Validation

↓

Swagger

↓

Tests

↓

Code Review

↓

Milestone 02 Finalizado
```

---

# Objetivos do Milestone

Este marco possui seis grandes objetivos.

## Objetivo 01

Criar todo o domínio Product.

---

## Objetivo 02

Implementar o catálogo de produtos.

---

## Objetivo 03

Validar relacionamentos entre entidades.

---

## Objetivo 04

Expandir os padrões arquiteturais definidos anteriormente.

---

## Objetivo 05

Reutilizar toda infraestrutura criada no Milestone 01.

---

## Objetivo 06

Preparar o projeto para os módulos de Inventory e Order.

---

# Escopo

Este Milestone contempla apenas o domínio Product.

Fazem parte deste marco:

- Product
- relacionamento Product → Category
- CRUD completo
- filtros
- paginação
- documentação
- testes

Não fazem parte:

- estoque;
- carrinho;
- pedidos;
- pagamentos;
- autenticação.

---

# Estrutura das Missões

## Missão 011 — Product Domain

### Objetivo

Implementar a camada de domínio.

### Entregáveis

- Product Entity
- ProductRepository
- Migration
- Specification
- Validator
- ADR correspondente

### Critérios de Aceite

✔ Entity criada.

✔ Relacionamento com Category.

✔ Migration funcionando.

✔ Repository implementado.

---

## Missão 012 — Product Service

### Objetivo

Implementar todas as regras de negócio.

### Entregáveis

- ProductService
- DTOs
- Mapper
- Regras comerciais

### Critérios de Aceite

✔ CRUD funcionando.

✔ Validações implementadas.

✔ Services desacopladas.

---

## Missão 013 — Product API

### Objetivo

Disponibilizar endpoints REST.

### Entregáveis

```
GET /products

GET /products/{id}

POST /products

PUT /products/{id}

DELETE /products/{id}
```

### Critérios de Aceite

✔ Endpoints funcionando.

✔ DTOs utilizados.

✔ HTTP Status corretos.

---

## Missão 014 — Product Search

### Objetivo

Implementar filtros e paginação.

### Entregáveis

- Specification
- Search API
- Paginação
- Ordenação

Exemplos:

```
GET /products?page=0

GET /products?category=uuid

GET /products?name=Notebook

GET /products?sort=name,asc
```

### Critérios de Aceite

✔ Busca dinâmica.

✔ Paginação.

✔ Ordenação.

---

## Missão 015 — Swagger

### Objetivo

Atualizar documentação OpenAPI.

### Entregáveis

- Endpoints documentados
- Exemplos
- Responses

### Critérios de Aceite

✔ Swagger atualizado.

---

## Missão 016 — Testes

### Objetivo

Garantir qualidade.

### Entregáveis

- Unit Tests
- Integration Tests
- Repository Tests

### Critérios de Aceite

✔ Cobertura mínima atingida.

---

## Missão 017 — Code Review

### Objetivo

Finalizar a Sprint.

### Entregáveis

- Refatorações
- Revisão
- Ajustes

### Critérios de Aceite

✔ Código aprovado.

✔ ADR atualizado.

✔ Documentação revisada.

---

# Estrutura Git

Durante este Milestone o fluxo será:

```
main

↓

sprint-002

↓

feature/mission-011-product-domain

↓

feature/mission-012-product-service

↓

feature/mission-013-product-api

↓

feature/mission-014-product-search

↓

feature/mission-015-swagger

↓

feature/mission-016-tests

↓

feature/mission-017-review
```

Cada missão possui sua própria Feature Branch.

---

# Organização dos Commits

Cada Feature deve conter commits pequenos e específicos.

Exemplos:

```
feat(product): create product entity

feat(product): create repository

feat(product): implement service

feat(product): add search specification

docs(adr): add product domain

test(product): add service tests
```

Nunca misturar documentação com implementação.

---

# Documentação Produzida

Durante este Milestone serão atualizados:

```
ADR

Architecture

API

Swagger

Roadmap

Mission Docs

Package Architecture
```

Toda alteração arquitetural deve possuir documentação correspondente.

---

# Critérios Gerais de Aceite

O Milestone será considerado concluído quando:

- Product completamente funcional;
- relacionamento com Category validado;
- endpoints REST implementados;
- paginação funcionando;
- filtros funcionando;
- documentação atualizada;
- testes aprovados;
- Code Review concluído.

---

# Fora do Escopo

Este Milestone não contempla:

- Inventory;
- Cart;
- Order;
- Payment;
- Notification;
- Authentication.

Esses módulos pertencem aos próximos marcos.

---

# Resultado Esperado

Ao concluir o Milestone 02 o Atlas Commerce possuirá:

- catálogo completo de produtos;
- arquitetura reutilizada com sucesso;
- dois módulos totalmente funcionais;
- documentação expandida;
- APIs padronizadas;
- base pronta para gerenciamento de estoque.

---

# Relação com Outros Documentos

Este documento complementa:

- ROADMAP.md
- MILESTONE-01.md
- API Documentation
- Architecture
- ADR-005 — Package by Feature
- ADR do módulo Product

---

# Benefícios

A conclusão deste Milestone proporciona:

- catálogo escalável;
- reutilização da arquitetura;
- consolidação do padrão Package by Feature;
- preparação para Inventory;
- maior maturidade da plataforma.

---

# Referências

- Domain Driven Design
- Clean Architecture
- Spring Boot Documentation
- Spring Data JPA
- REST API Design

---

# Próximo Capítulo

roadmap/RELEASES.md