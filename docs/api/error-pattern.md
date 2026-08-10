# Padrão de Erros da API

---

# Objetivo

Definir o padrão oficial de tratamento de erros utilizado pelo Atlas Commerce.

Ao final deste capítulo o desenvolvedor será capaz de compreender:

- como a API responde quando ocorre um erro
- diferenças entre erros de negócio e erros técnicos
- estrutura oficial das respostas JSON
- códigos HTTP utilizados
- tratamento global de exceções
- padronização das mensagens retornadas ao cliente

Este documento estabelece um contrato único para todas as respostas de erro da API.

---

# Contexto

Toda aplicação está sujeita a falhas.

Essas falhas podem ocorrer por diversos motivos.

Exemplos:

- recurso inexistente
- dados inválidos
- usuário sem permissão
- token expirado
- erro interno
- violação de regras de negócio

Quando não existe um padrão, cada Controller retorna erros diferentes.

Isso dificulta:

- integração
- documentação
- manutenção
- depuração
- experiência do desenvolvedor

Por esse motivo o Atlas Commerce define um único formato de resposta.

---

# Motivação

Imagine que dois endpoints retornem erros diferentes.

Primeiro endpoint:

```json
{
    "error":"Category not found"
}
```

Segundo endpoint:

```json
{
    "message":"Produto inexistente."
}
```

Terceiro endpoint:

```json
{
    "status":404
}
```

Embora todos representem o mesmo tipo de problema, cada um possui uma estrutura diferente.

Essa inconsistência obriga clientes a tratar cada endpoint individualmente.

O Atlas Commerce elimina esse problema utilizando um único contrato.

---

# Estrutura Oficial

Toda resposta de erro deverá seguir exatamente o formato abaixo.

```json
{
    "timestamp":"2026-08-06T15:30:15Z",
    "status":404,
    "error":"Not Found",
    "message":"Category not found.",
    "path":"/api/v1/categories/8d2c..."
}
```

---

# Campos da Resposta

| Campo | Descrição |
|--------|-----------|
| timestamp | Data e hora do erro |
| status | Código HTTP |
| error | Nome oficial do erro HTTP |
| message | Mensagem amigável |
| path | Endpoint que originou o erro |

---

# Fluxo do Tratamento

```
Cliente

↓

Controller

↓

Service

↓

Exception

↓

GlobalExceptionHandler

↓

JSON Padronizado

↓

Cliente
```

Todo erro deve passar pelo Global Exception Handler.

Nenhum Controller deve montar respostas manualmente.

---

# Tratamento Global

O Atlas Commerce utilizará um único componente responsável pelo tratamento das exceções.

```
GlobalExceptionHandler
```

Ele será responsável por:

- capturar exceções
- converter para JSON
- definir código HTTP
- padronizar mensagens

Isso garante consistência em toda a API.

---

# Categorias de Erros

Os erros são classificados em grupos.

## Erros do Cliente (4xx)

Representam problemas enviados pelo consumidor da API.

Exemplos:

- dados inválidos
- recurso inexistente
- autenticação inválida
- permissão insuficiente

---

## Erros do Servidor (5xx)

Representam falhas internas.

Exemplos:

- erro inesperado
- banco indisponível
- falha de integração
- timeout

Esses erros nunca devem expor detalhes internos da aplicação.

---

# Principais Códigos HTTP

| Código | Significado |
|---------|-------------|
| 400 | Bad Request |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |
| 405 | Method Not Allowed |
| 409 | Conflict |
| 422 | Unprocessable Entity |
| 500 | Internal Server Error |
| 503 | Service Unavailable |

---

# Erro 400

Utilizado quando os dados enviados pelo cliente são inválidos.

Exemplo:

```json
{
    "timestamp":"...",
    "status":400,
    "error":"Bad Request",
    "message":"Invalid request body.",
    "path":"/api/v1/categories"
}
```

---

# Erro 401

O usuário não está autenticado.

Exemplo:

```json
{
    "status":401,
    "error":"Unauthorized",
    "message":"Authentication required.",
    "path":"/api/v1/categories"
}
```

---

# Erro 403

Usuário autenticado, porém sem permissão.

```json
{
    "status":403,
    "error":"Forbidden",
    "message":"Access denied.",
    "path":"/api/v1/categories"
}
```

---

# Erro 404

Recurso não encontrado.

```json
{
    "status":404,
    "error":"Not Found",
    "message":"Category not found.",
    "path":"/api/v1/categories/15"
}
```

---

# Erro 409

Conflito de negócio.

Exemplo:

Categoria com o mesmo nome já cadastrada.

```json
{
    "status":409,
    "error":"Conflict",
    "message":"Category already exists.",
    "path":"/api/v1/categories"
}
```

---

# Erro 422

Erro de validação.

Exemplo:

```json
{
    "timestamp":"...",
    "status":422,
    "error":"Validation Error",
    "message":"Validation failed.",
    "path":"/api/v1/categories",
    "errors":[
        {
            "field":"name",
            "message":"must not be blank"
        },
        {
            "field":"description",
            "message":"size must be between 5 and 255"
        }
    ]
}
```

O campo **errors** poderá conter uma lista detalhada das violações encontradas.

---

# Erro 500

Erro inesperado.

Nunca retornar StackTrace.

Nunca retornar Exception completa.

Exemplo:

```json
{
    "status":500,
    "error":"Internal Server Error",
    "message":"Unexpected error.",
    "path":"/api/v1/categories"
}
```

---

# Fluxo de Validação

```
Request

↓

Validation

↓

Business Rules

↓

Repository

↓

Database

↓

Response
```

Caso qualquer etapa gere exceção, o Global Exception Handler será responsável por construir a resposta.

---

# Exceções Personalizadas

Cada módulo poderá possuir exceções específicas.

Exemplo:

```
CategoryNotFoundException

ProductNotFoundException

OrderNotFoundException

DuplicateCategoryException

BusinessException

ValidationException
```

Essas exceções representam regras de negócio e facilitam a manutenção do código.

---

# Estrutura Recomendada

```
exception

├── GlobalExceptionHandler
├── ApiErrorResponse
├── BusinessException
├── ValidationException
├── ResourceNotFoundException
├── UnauthorizedException
└── ConflictException
```

Cada classe possui uma responsabilidade única.

---

# Decisão Arquitetural

Esta estratégia está relacionada às ADRs:

- ADR-000 — Arquitetura do Projeto
- ADR-004 — Repository Pattern
- ADR-006 — Category Domain

---

# Boas Práticas

✔ Utilizar códigos HTTP corretos.

✔ Nunca retornar StackTrace.

✔ Mensagens devem ser claras.

✔ Centralizar tratamento em um único Handler.

✔ Utilizar exceções específicas para regras de negócio.

✔ Manter o mesmo formato JSON em toda a API.

---

# Erros Comuns

❌ Retornar Exception diretamente.

❌ Expor detalhes internos da aplicação.

❌ Utilizar HTTP 200 para erros.

❌ Criar formatos diferentes entre Controllers.

❌ Misturar mensagens técnicas com mensagens para o usuário.

---

# Referências

- RFC 9110 — HTTP Semantics
- RFC 7807 — Problem Details for HTTP APIs
- Spring Boot Exception Handling
- Spring Validation
- OWASP Error Handling Cheat Sheet

---

# Próximo Capítulo

pagination.md

No próximo capítulo será definida a estratégia oficial de paginação do Atlas Commerce, incluindo ordenação, filtros, limites, metadados das respostas e boas práticas para consultas eficientes em grandes volumes de dados.