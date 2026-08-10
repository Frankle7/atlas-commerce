# Atlas Commerce API

> Versão: 1.0.0  
> Última atualização: Agosto/2026

---

# Objetivo

Este documento define os padrões oficiais utilizados pela API REST do Atlas Commerce.

Toda implementação realizada durante o desenvolvimento deverá seguir as convenções descritas neste documento.

A API foi projetada para ser consistente, previsível, escalável e de fácil integração com aplicações Web, Mobile e serviços externos.

Este documento serve como referência para desenvolvedores Backend, Frontend, Mobile e equipes responsáveis por integrações.

---

# Contexto

O Atlas Commerce foi desenvolvido utilizando Spring Boot e segue os princípios da arquitetura RESTful.

Toda comunicação entre cliente e servidor acontece através do protocolo HTTP utilizando mensagens no formato JSON.

A API é Stateless, versionada e organizada por domínio de negócio.

Cada módulo possui sua própria camada Controller, Service, Repository e DTO, garantindo baixo acoplamento e alta coesão.

---

# Motivação

A definição de padrões antes da implementação reduz inconsistências entre módulos e facilita a manutenção do sistema ao longo do tempo.

Os principais objetivos são:

- Padronizar toda comunicação HTTP
- Garantir previsibilidade para consumidores da API
- Facilitar evolução sem quebrar clientes existentes
- Melhorar documentação
- Permitir geração automática de documentação OpenAPI

---

# Princípios da API

A API do Atlas Commerce segue os seguintes princípios:

- RESTful
- Stateless
- Resource Oriented
- JSON First
- Versionada
- Idempotente quando aplicável
- Segura
- Escalável
- Documentada

---

# Arquitetura da Requisição

Todo fluxo de uma requisição segue exatamente a estrutura abaixo.

```
Cliente

      │
      ▼

HTTP Request

      │
      ▼

Controller

      │
      ▼

DTO

      │
      ▼

Validation

      │
      ▼

Service

      │
      ▼

Repository

      │
      ▼

PostgreSQL

      │
      ▼

Repository

      │
      ▼

Service

      │
      ▼

Response DTO

      │
      ▼

HTTP Response
```

---

# Convenções REST

Cada recurso da API representa um domínio do sistema.

Exemplo:

```
Categories
Products
Orders
Users
Inventory
Payments
Cart
Authentication
Notifications
```

Cada recurso possui uma URL própria.

Exemplo:

```
GET     /api/v1/categories

GET     /api/v1/categories/{id}

POST    /api/v1/categories

PUT     /api/v1/categories/{id}

DELETE  /api/v1/categories/{id}
```

---

# Métodos HTTP

## GET

Utilizado para consultas.

Nunca altera estado da aplicação.

Exemplo

```
GET /api/v1/categories
```

---

## POST

Utilizado para criação de recursos.

Exemplo

```
POST /api/v1/categories
```

---

## PUT

Atualização completa.

Exemplo

```
PUT /api/v1/categories/{id}
```

---

## PATCH

Atualização parcial.

Utilizado apenas quando necessário.

---

## DELETE

Remove um recurso.

```
DELETE /api/v1/categories/{id}
```

---

# Formato JSON

Todas as requisições e respostas utilizam JSON.

Exemplo

```json
{
    "id":"7d75d9d0-6e3d-4b70-b83d-5d06dbcb70df",
    "name":"Electronics"
}
```

---

# Content-Type

Todas as requisições devem utilizar

```
application/json
```

---

# Charset

UTF-8

---

# Datas

O padrão utilizado é ISO-8601.

Exemplo

```
2026-08-06T15:30:45Z
```

---

# UUID

Todos os identificadores do sistema utilizam UUID.

Exemplo

```
ad2a3db4-11df-4f52-80ba-b4de12c51101
```

---

# Headers

Headers obrigatórios.

```
Content-Type: application/json

Accept: application/json
```

Quando autenticado.

```
Authorization: Bearer eyJhbGc...
```

---

# Versionamento

Toda URL inicia com a versão da API.

```
/api/v1/
```

Exemplo

```
GET /api/v1/products

GET /api/v1/orders

GET /api/v1/categories
```

Mais detalhes em:

```
versioning.md
```

---

# Estrutura de Resposta

Resposta de sucesso

```json
{
    "id":"uuid",
    "name":"Electronics"
}
```

Resposta de erro

```json
{
    "timestamp":"2026-08-06T18:40:21Z",
    "status":404,
    "error":"Not Found",
    "message":"Category not found",
    "path":"/api/v1/categories/1"
}
```

---

# Códigos HTTP

| Código | Significado |
|---------|-------------|
| 200 | OK |
| 201 | Created |
| 202 | Accepted |
| 204 | No Content |
| 400 | Bad Request |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |
| 409 | Conflict |
| 422 | Validation Error |
| 500 | Internal Server Error |

---

# Estrutura Modular

Cada domínio possui seu próprio módulo.

```
category/

product/

inventory/

order/

payment/

user/

cart/

notification/
```

Todos seguem exatamente a mesma estrutura.

```
controller

dto

entity

mapper

repository

service

validator

specification
```

---

# Convenções Gerais

Toda Entity possui DTO.

Toda regra de negócio fica na Service.

Controllers não possuem lógica de negócio.

Repositories apenas acessam dados.

DTO nunca representa tabela do banco.

Responses nunca retornam Entity.

---

# Segurança

Toda autenticação será realizada utilizando JWT.

Endpoints públicos serão mínimos.

Endpoints privados exigirão Bearer Token.

Mais detalhes em:

```
authentication.md
```

---

# Paginação

Toda listagem suporta paginação.

Exemplo

```
GET /api/v1/categories?page=0&size=20&sort=name,asc
```

Mais detalhes em

```
pagination.md
```

---

# Tratamento de Erros

Todos os erros seguem exatamente o mesmo padrão JSON.

Nunca serão retornadas exceções Java diretamente para o cliente.

Mais detalhes em

```
error-pattern.md
```

---

# Decisões Arquiteturais

Esta documentação está diretamente relacionada às seguintes ADRs.

- ADR-001 PostgreSQL
- ADR-002 JWT
- ADR-003 UUID
- ADR-004 Repository Pattern
- ADR-005 Package by Feature

---

# Boas Práticas

- Nunca expor Entity diretamente
- Sempre utilizar DTO
- Sempre utilizar ResponseEntity
- Nunca quebrar contratos existentes
- Sempre utilizar UUID
- Documentar todos os endpoints
- Versionar toda alteração incompatível

---

# Erros Comuns

❌ Retornar Entity diretamente

❌ Misturar regra de negócio no Controller

❌ Utilizar Integer como identificador

❌ Criar endpoints sem documentação

❌ Quebrar contratos sem criar nova versão

---

# Referências

- REST Architectural Style
- RFC 9110 HTTP Semantics
- Spring Boot Documentation
- Spring Web MVC
- OpenAPI Specification
- JSON RFC 8259

---

# Próximo Capítulo

→ versioning.md

Neste capítulo será apresentada a estratégia oficial de versionamento adotada pelo Atlas Commerce, os critérios para evolução da API e como evitar breaking changes.