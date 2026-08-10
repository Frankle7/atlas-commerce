
---

# `docs/missions/MISSION-003.md`

Essa aqui temos definida com bastante precisão: **PostgreSQL Foundation**.

Copie:

```markdown
# MISSION-003 — PostgreSQL Foundation

## Nome

PostgreSQL Foundation

---

## Objetivo

Modelar fisicamente o banco de dados do Atlas Commerce.

---

## Contexto

O domínio do sistema já foi definido nas etapas anteriores.

A arquitetura também estabeleceu o PostgreSQL como banco de dados principal.

Agora é necessário transformar o modelo conceitual em uma estrutura física executável.

Esta missão estabelece a fundação do banco de dados que será utilizada pelas próximas Features.

---

## Motivação

A aplicação depende de uma camada de persistência confiável e reproduzível.

O banco precisa:

- iniciar de forma consistente
- possuir controle de versões
- permitir execução automatizada das alterações
- possuir constraints adequadas
- utilizar identificadores UUID
- permitir evolução incremental do schema

Por isso, o Atlas Commerce utiliza PostgreSQL juntamente com Docker e Flyway.

---

## Escopo

A missão contempla a preparação da infraestrutura inicial do banco de dados.

```text
Docker
   ↓
PostgreSQL
   ↓
Flyway
   ↓
Migration
   ↓
Database Schema