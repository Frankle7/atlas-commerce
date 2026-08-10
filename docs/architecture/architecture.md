# Arquitetura do Atlas Commerce

---

# Objetivo

Definir a arquitetura oficial utilizada pelo Atlas Commerce.

Ao final deste capítulo o desenvolvedor será capaz de compreender:

- a visão arquitetural do sistema
- como os módulos se relacionam
- organização em camadas
- princípios utilizados
- responsabilidades de cada componente
- fluxo completo de uma requisição
- decisões arquiteturais adotadas

Este documento é considerado o coração técnico do projeto.

---

# Contexto

O Atlas Commerce foi desenvolvido para servir como uma plataforma moderna de e-commerce, priorizando:

- escalabilidade
- manutenibilidade
- modularidade
- legibilidade
- baixo acoplamento
- alta coesão

A arquitetura foi projetada para suportar evolução contínua sem comprometer a estabilidade da aplicação.

---

# Motivação

Projetos que crescem sem uma arquitetura definida tendem a apresentar problemas como:

- classes gigantes
- duplicação de código
- dependências circulares
- dificuldade para testes
- dificuldade para adicionar novas funcionalidades

O Atlas Commerce adota uma arquitetura em camadas combinada com **Package by Feature**, permitindo que cada domínio evolua de forma independente.

---

# Visão Geral

```
                 Atlas Commerce

                        │

        ┌───────────────┼───────────────┐

        │               │               │

     Frontend         Backend       PostgreSQL

        │               │               │

        └───────────────┼───────────────┘

                        │

                    Docker Compose
```

Todo o ecossistema é executado localmente utilizando Docker.

---

# Arquitetura Geral

```
Cliente

        │

HTTP Request

        │

Controller

        │

Service

        │

Repository

        │

PostgreSQL
```

Cada camada possui responsabilidade única.

Nenhuma camada deve assumir responsabilidades pertencentes a outra.

---

# Arquitetura em Camadas

O backend segue a arquitetura em camadas (Layered Architecture).

```
Presentation

↓

Application

↓

Domain

↓

Persistence

↓

Database
```

---

# Camada de Apresentação

Responsável pela comunicação HTTP.

Contém:

- Controllers
- DTOs
- Validação de entrada
- Conversão de objetos

Essa camada nunca implementa regras de negócio.

---

# Camada de Aplicação

Representada pelos Services.

Responsabilidades:

- orquestrar casos de uso
- aplicar regras de negócio
- coordenar chamadas ao repositório
- controlar transações

---

# Camada de Persistência

Representada pelos Repositories.

Responsabilidades:

- consultas ao banco
- persistência de entidades
- abstração do acesso aos dados

Toda comunicação com o PostgreSQL ocorre através dessa camada.

---

# Banco de Dados

O PostgreSQL é responsável por armazenar todas as informações persistentes.

Entre elas:

- usuários
- categorias
- produtos
- pedidos
- estoque
- pagamentos
- carrinho

---

# Organização por Feature

Ao invés de separar o projeto por tecnologia, o Atlas Commerce utiliza **Package by Feature**.

```
com.atlascommerce

├── category
├── product
├── order
├── payment
├── inventory
├── user
├── cart
├── address
├── auth
├── notification
├── common
├── config
├── security
└── shared
```

Cada módulo representa um domínio do negócio.

---

# Estrutura Interna de um Módulo

Todos os módulos seguem exatamente a mesma organização.

```
category

├── controller
├── dto
├── entity
├── mapper
├── repository
├── service
├── specification
└── validator
```

Essa padronização reduz a curva de aprendizado e facilita a navegação pelo código.

---

# Responsabilidade de Cada Pacote

## controller

Recebe requisições HTTP e devolve respostas.

Nunca implementa regras de negócio.

---

## dto

Define os contratos da API.

Controla os dados enviados e recebidos.

---

## entity

Representa as tabelas do banco de dados.

Utiliza JPA/Hibernate.

---

## mapper

Realiza conversões entre Entity e DTO.

---

## repository

Comunica-se diretamente com o banco de dados.

Utiliza Spring Data JPA.

---

## service

Implementa as regras de negócio.

É a camada central da aplicação.

---

## specification

Contém consultas dinâmicas e filtros complexos.

---

## validator

Centraliza validações específicas do domínio.

---

# Fluxo Completo de uma Requisição

```
Cliente

↓

Controller

↓

DTO

↓

Service

↓

Validator

↓

Repository

↓

PostgreSQL

↓

Repository

↓

Service

↓

Mapper

↓

DTO

↓

Controller

↓

Resposta JSON
```

Esse fluxo representa o caminho padrão percorrido por qualquer requisição.

---

# Dependências Entre Camadas

```
Controller

↓

Service

↓

Repository

↓

Database
```

As dependências são sempre unidirecionais.

Uma camada nunca deve depender de uma camada superior.

---

# Princípios Arquiteturais

O Atlas Commerce foi construído seguindo os seguintes princípios:

- Separation of Concerns
- Single Responsibility Principle
- Dependency Inversion
- DRY
- KISS
- Clean Code
- Clean Architecture (adaptada)
- Package by Feature

Esses princípios orientam todas as decisões de projeto.

---

# Escalabilidade

Novos módulos podem ser adicionados sem alterar os existentes.

Exemplo:

```
wishlist

review

coupon

shipping

invoice
```

Cada novo domínio segue a mesma estrutura dos módulos atuais.

---

# Benefícios da Arquitetura

- baixo acoplamento
- alta coesão
- facilidade para testes
- facilidade de manutenção
- organização previsível
- evolução incremental
- reutilização de componentes
- facilidade para novos desenvolvedores

---

# Decisões Arquiteturais

Esta arquitetura é sustentada pelas seguintes ADRs:

- ADR-000 — Arquitetura do Projeto
- ADR-003 — UUID
- ADR-004 — Repository Pattern
- ADR-005 — Package by Feature
- ADR-006 — Category Domain

---

# Boas Práticas

✔ Manter cada classe com uma única responsabilidade.

✔ Evitar dependências entre módulos.

✔ Utilizar DTOs para comunicação externa.

✔ Centralizar regras de negócio nos Services.

✔ Manter Controllers enxutos.

✔ Utilizar Repository apenas para acesso a dados.

✔ Padronizar a estrutura de todos os módulos.

---

# Erros Comuns

❌ Colocar regras de negócio no Controller.

❌ Acessar Repository diretamente pelo Controller.

❌ Misturar Entity com DTO.

❌ Criar dependências circulares.

❌ Duplicar regras de negócio em diferentes módulos.

❌ Criar módulos com estruturas diferentes do padrão.

---

# Referências

- Clean Architecture — Robert C. Martin
- Domain-Driven Design — Eric Evans
- Spring Boot Reference Documentation
- Spring Data JPA
- Martin Fowler — Patterns of Enterprise Application Architecture

---

# Próximo Capítulo

package-architecture.md

No próximo capítulo será detalhada a arquitetura interna dos pacotes do Atlas Commerce, explicando em profundidade a responsabilidade de cada diretório, suas dependências permitidas e as regras de organização do código.