# Database Architecture

> Atlas Commerce Technical Book
>
> Capítulo 12 — Arquitetura do Banco de Dados

---

# Objetivo

Explicar toda a arquitetura do banco de dados do Atlas Commerce.

Este documento apresenta a filosofia utilizada na modelagem, os princípios adotados, as decisões arquiteturais, as boas práticas e a organização das entidades que sustentam toda a aplicação.

Mais do que listar tabelas, este capítulo explica por que cada decisão foi tomada.

---

# Contexto

Todo software orientado a negócios depende da qualidade da modelagem dos seus dados.

Uma arquitetura mal planejada gera:

- duplicidade de informações;
- inconsistência de dados;
- dificuldade de manutenção;
- baixo desempenho;
- regras de negócio espalhadas.

No Atlas Commerce, o banco de dados foi projetado para refletir o domínio do negócio e acompanhar o crescimento da aplicação.

---

# Filosofia da Modelagem

A arquitetura segue alguns princípios fundamentais.

## Banco orientado ao domínio

O banco representa o negócio.

Não representa telas.

Não representa APIs.

Não representa casos de uso específicos.

Cada entidade existe porque representa um conceito do domínio.

Exemplos:

```
Category

Product

Customer

Order

Payment

Address
```

---

## Responsabilidade única

Cada tabela possui apenas uma responsabilidade.

Exemplo

Category

Responsável apenas pelas categorias.

Não armazena produtos.

Não armazena estoque.

Não armazena pedidos.

---

## Integridade dos dados

O banco garante consistência através de:

- chaves primárias
- foreign keys
- índices
- constraints
- unique keys
- validações

Sempre que possível, as regras devem ser protegidas pelo próprio banco.

---

# Organização Geral

```
Atlas Commerce

│
├── Category
├── Product
├── Inventory
├── Customer
├── Address
├── Cart
├── Order
├── Payment
├── Notification
├── Auth
└── Security
```

Cada módulo possui suas próprias tabelas.

---

# Arquitetura por Domínio

```
Category
        │
        ▼
Product
        │
        ▼
Inventory

Customer
        │
        ▼
Address

Customer
        │
        ▼
Cart
        │
        ▼
Order
        │
        ▼
Payment
```

Cada módulo depende apenas do domínio imediatamente relacionado.

---

# Padrão de Identificação

Todas as entidades utilizam UUID como chave primária.

Exemplo

```
id UUID PRIMARY KEY
```

---

## Por que UUID?

Vantagens

- unicidade global;
- geração distribuída;
- segurança;
- não expõe quantidade de registros;
- facilita microsserviços.

---

# Auditoria

Todas as entidades seguem um padrão comum.

```
id

created_at

updated_at

deleted_at (quando necessário)
```

---

## Exemplo

```
Category

id

name

description

active

created_at

updated_at
```

---

# Soft Delete

Nem todas as entidades devem ser removidas fisicamente.

Algumas utilizam Soft Delete.

Exemplo

```
deleted_at

deleted_by
```

Benefícios

- histórico;
- auditoria;
- recuperação de dados.

---

# Relacionamentos

Relacionamentos utilizam Foreign Keys.

Exemplo

```
Category

1
│
│
N
Product
```

Outro exemplo

```
Customer

1
│
│
N
Order
```

---

# Normalização

O projeto segue principalmente a Terceira Forma Normal (3FN).

Objetivos

- eliminar redundância;
- evitar inconsistências;
- facilitar manutenção.

Em casos específicos, pequenas desnormalizações poderão ser adotadas por motivos de desempenho.

---

# Índices

Os índices são criados para otimizar consultas frequentes.

Exemplos

```
Category.name

Product.sku

Product.name

Order.customer_id

Order.created_at
```

---

# Constraints

O banco utiliza constraints para proteger a integridade.

Exemplos

```
NOT NULL

UNIQUE

CHECK

FOREIGN KEY
```

---

# Convenções de Nomenclatura

Tabelas

```
snake_case
```

Exemplo

```
customer_address

order_item
```

Colunas

```
snake_case
```

Exemplo

```
created_at

updated_at

category_id
```

---

# Convenções para Chaves

Primary Key

```
id
```

Foreign Key

```
category_id

product_id

customer_id

order_id
```

Nunca utilizar nomes inconsistentes.

---

# Migrações

Toda alteração estrutural deve ocorrer através do Flyway.

Exemplo

```
V001__create_category_table.sql

V002__create_product_table.sql

V003__create_customer_table.sql
```

Nunca alterar migrações já executadas.

Sempre criar uma nova versão.

---

# Evolução do Banco

Fluxo

```
Nova Feature

↓

Nova Migration

↓

Review

↓

Merge

↓

Deploy

↓

Banco atualizado
```

---

# Diagramas

Arquitetura Geral

```
                 Category
                      │
                      ▼
                 Product
                      │
                      ▼
                 Inventory


Customer ─────► Address
      │
      ▼
     Cart
      │
      ▼
    Order
      │
      ▼
   Payment
```

---

Fluxo das Migrações

```
Developer

↓

Migration SQL

↓

Flyway

↓

Database

↓

Application
```

---

# Decisões Arquiteturais

Este documento está relacionado aos ADRs:

- ADR-001 — PostgreSQL
- ADR-003 — UUID
- ADR-004 — Repository Pattern
- ADR-006 — Category Domain

---

# Boas Práticas

✓ Nunca alterar migrations antigas.

✓ Toda mudança estrutural gera uma nova migration.

✓ Utilizar UUID em todas as entidades.

✓ Sempre definir índices importantes.

✓ Utilizar Foreign Keys.

✓ Modelar o domínio antes das tabelas.

✓ Evitar duplicação de dados.

✓ Nomear tabelas de forma consistente.

✓ Centralizar regras de integridade no banco quando apropriado.

---

# Erros Comuns

❌ Criar tabelas baseadas em telas.

❌ Usar IDs incrementais sem necessidade.

❌ Alterar migrations antigas.

❌ Criar relacionamentos sem Foreign Key.

❌ Duplicar informações em múltiplas tabelas.

❌ Não criar índices.

❌ Misturar regras de negócio com estrutura de armazenamento.

---

# Referências

- PostgreSQL Documentation
- Flyway Documentation
- Database Design for Mere Mortals
- Designing Data-Intensive Applications
- Domain-Driven Design — Eric Evans

---

# Próximo Capítulo

onboarding/project-structure.md