# Autenticação

---

# Objetivo

Definir a estratégia oficial de autenticação e autorização utilizada pelo Atlas Commerce.

Ao final deste capítulo o desenvolvedor será capaz de compreender:

- como funciona o fluxo de autenticação
- como o JWT será utilizado
- diferenças entre autenticação e autorização
- como proteger endpoints
- como ocorre a validação do token
- responsabilidades da camada Security

Este documento estabelece o padrão oficial de segurança da API.

---

# Contexto

Um sistema de e-commerce manipula informações sensíveis.

Entre elas:

- dados pessoais
- pedidos
- pagamentos
- endereços
- carrinhos
- estoque
- informações administrativas

Permitir acesso irrestrito colocaria todo o sistema em risco.

Por esse motivo o Atlas Commerce adota autenticação baseada em JWT (JSON Web Token).

---

# Motivação

Uma API pública precisa responder duas perguntas antes de executar qualquer operação.

1. Quem é o usuário?

2. Esse usuário possui permissão para executar esta ação?

Essas perguntas representam dois conceitos diferentes.

Autenticação

↓

Identificar quem está acessando.

Autorização

↓

Definir o que esse usuário pode fazer.

---

# Conceitos Fundamentais

## Autenticação

É o processo de confirmar a identidade do usuário.

Exemplo

```
Email

+

Senha

↓

Usuário autenticado
```

Após a autenticação o sistema gera um Token JWT.

---

## Autorização

Depois de autenticado o sistema verifica as permissões.

Exemplo

```
ADMIN

↓

Pode criar categorias

Pode excluir produtos

Pode gerenciar usuários
```

```
CUSTOMER

↓

Pode visualizar produtos

Pode realizar pedidos

Pode atualizar seu perfil
```

---

# Arquitetura da Segurança

```
Client

↓

POST /login

↓

AuthenticationController

↓

AuthenticationService

↓

UserRepository

↓

PasswordEncoder

↓

JWT Generator

↓

JWT Token
```

Após a autenticação o cliente utilizará esse token em todas as requisições.

---

# Fluxo Completo

```
Cliente

↓

Login

↓

Email + Senha

↓

Spring Security

↓

AuthenticationManager

↓

UserDetailsService

↓

PasswordEncoder

↓

JWT

↓

Resposta
```

---

# Estrutura do Token

Exemplo

```
eyJhbGciOiJIUzI1NiIs...

```

O token contém informações como:

- id do usuário
- e-mail
- permissões
- data de expiração

Essas informações são assinadas digitalmente.

O cliente não deve alterar seu conteúdo.

---

# Enviando o Token

Toda requisição autenticada deve utilizar o cabeçalho Authorization.

Exemplo

```
Authorization: Bearer eyJhbGciOiJIUzI1NiIs...
```

---

# Fluxo das Requisições

```
Client

↓

Authorization Header

↓

JWT Filter

↓

Token Validation

↓

Security Context

↓

Controller

↓

Service

↓

Repository
```

Caso o token seja inválido a requisição é encerrada antes de chegar ao Controller.

---

# Endpoints Públicos

Alguns endpoints não exigem autenticação.

Exemplo

```
POST /api/v1/auth/login

POST /api/v1/auth/register

GET /swagger-ui

GET /v3/api-docs
```

---

# Endpoints Protegidos

Todos os demais recursos exigem autenticação.

Exemplo

```
GET /categories

POST /categories

PUT /products

DELETE /orders
```

---

# Controle de Permissões

O Atlas Commerce utilizará autorização baseada em Roles.

Exemplo

```
ROLE_ADMIN
ROLE_MANAGER
ROLE_CUSTOMER
```

Cada endpoint poderá restringir acesso.

Exemplo

```
@PreAuthorize("hasRole('ADMIN')")
```

ou

```
@PreAuthorize("hasAnyRole('ADMIN','MANAGER')")
```

---

# Tempo de Expiração

Os tokens possuem validade limitada.

Exemplo

```
Access Token

↓

2 horas
```

Após expirar será necessário realizar novo login.

---

# Renovação do Token

Em versões futuras poderá ser utilizado Refresh Token.

Fluxo

```
Access Token expirado

↓

Refresh Token

↓

Novo Access Token
```

Essa funcionalidade será implementada em uma missão futura.

---

# Estrutura do Módulo Security

```
security

├── config
├── filter
├── jwt
├── service
├── model
├── exception
└── util
```

Cada pacote possui responsabilidade única.

---

# Integração com Spring Security

O Atlas Commerce utilizará:

- Spring Security
- AuthenticationManager
- PasswordEncoder
- BCrypt
- UserDetailsService
- SecurityFilterChain

Esses componentes formam a base da camada de autenticação.

---

# Exemplo de Fluxo

```
Cliente

↓

POST /login

↓

JWT

↓

Bearer Token

↓

GET /categories

↓

JWT Filter

↓

Controller

↓

Resposta
```

---

# Decisão Arquitetural

Esta estratégia está relacionada às ADRs:

- ADR-002 — JWT Authentication
- ADR-004 — Repository Pattern
- ADR-005 — Package by Feature

---

# Boas Práticas

✔ Utilizar HTTPS em produção.

✔ Nunca armazenar senha em texto puro.

✔ Utilizar BCrypt.

✔ Nunca expor informações sensíveis no JWT.

✔ Utilizar expiração curta para Access Token.

✔ Validar todas as requisições autenticadas.

✔ Centralizar regras de segurança.

---

# Erros Comuns

❌ Armazenar senha sem criptografia.

❌ Colocar dados sensíveis dentro do JWT.

❌ Esquecer de validar expiração.

❌ Permitir endpoints administrativos sem autorização.

❌ Misturar autenticação com regras de negócio.

---

# Referências

- Spring Security Reference
- JWT RFC 7519
- OWASP Authentication Cheat Sheet
- OAuth 2.0 Concepts
- Spring Authorization Server

---

# Próximo Capítulo

error-pattern.md

No próximo capítulo será definido o padrão oficial de respostas de erro do Atlas Commerce, incluindo tratamento global de exceções, estrutura JSON, códigos HTTP e padronização das mensagens retornadas pela API.