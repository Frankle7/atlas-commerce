
---

# `docs/adr/ADR-002-jwt.md`

```markdown
# ADR-002 — JWT como Estratégia de Autenticação

## Status

Accepted

---

## Objetivo

Definir a estratégia de autenticação utilizada pelo Atlas Commerce.

---

## Contexto

O Atlas Commerce possui recursos que exigem autenticação e autorização.

Entre eles:

- usuários
- pedidos
- carrinho
- pagamentos
- dados privados

A API precisa identificar o usuário autenticado e controlar o acesso aos recursos protegidos.

---

## Problema

Precisamos escolher uma estratégia de autenticação que:

- funcione bem com APIs REST
- seja adequada para aplicações distribuídas
- não dependa de sessão armazenada no servidor
- possa ser integrada ao Spring Security
- permita controle de autorização

---

## Opções Consideradas

- Session-based Authentication
- JWT
- OAuth 2.0

---

## Decisão

O Atlas Commerce utilizará **JWT (JSON Web Token)** como estratégia de autenticação baseada em tokens.

---

## Funcionamento

Fluxo simplificado:

```text
Client
   │
   │ Login
   ▼
Authentication
   │
   ▼
JWT
   │
   ▼
Client
   │
   │ Authorization: Bearer <token>
   ▼
API
   │
   ▼
Security Filter
   │
   ▼
Controller