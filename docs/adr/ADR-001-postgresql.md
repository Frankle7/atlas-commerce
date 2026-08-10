
---

# `docs/adr/ADR-001-postgresql.md`

```markdown
# ADR-001 — PostgreSQL como Banco de Dados

## Status

Accepted

---

## Objetivo

Definir o banco de dados relacional oficial utilizado pelo Atlas Commerce.

---

## Contexto

O Atlas Commerce necessita de um sistema de persistência confiável para armazenar dados relacionados aos seus domínios de negócio.

Entre os principais domínios estão:

- Category
- Product
- Inventory
- Order
- Payment
- User
- Cart

O banco precisa oferecer:

- consistência
- integridade referencial
- transações
- suporte a relacionamentos
- boa integração com Java e Spring Boot
- capacidade de evolução

---

## Opções Consideradas

Foram consideradas diferentes alternativas de persistência.

Entre elas:

- PostgreSQL
- MySQL
- MongoDB

---

## Decisão

O PostgreSQL será utilizado como banco de dados relacional oficial do Atlas Commerce.

---

## Justificativa

### Banco Relacional

O domínio possui diversas relações entre entidades.

Exemplo:

```text
Category
   ↓
Product
   ↓
Order
   ↓
Payment