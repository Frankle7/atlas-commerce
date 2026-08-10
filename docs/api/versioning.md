# Versionamento da API

---

# Objetivo

Definir a estratégia oficial de versionamento utilizada pelo Atlas Commerce.

Ao final deste capítulo o desenvolvedor será capaz de compreender:

- como funciona o versionamento da API
- quando criar uma nova versão
- quando NÃO criar uma nova versão
- como manter compatibilidade entre clientes
- como evoluir contratos REST sem quebrar integrações

Este documento estabelece a política oficial de evolução da API.

---

# Contexto

Nenhuma API permanece igual para sempre.

Novos recursos são adicionados.

Campos são criados.

Endpoints deixam de existir.

Regras de negócio evoluem.

Sem uma estratégia de versionamento bem definida, qualquer alteração pode quebrar aplicações que já utilizam a API.

O versionamento permite que diferentes clientes continuem funcionando enquanto novas funcionalidades são desenvolvidas.

---

# Motivação

Imagine o seguinte cenário:

A versão atual da API retorna:

```json
{
    "id":"8d1e",
    "name":"Electronics"
}
```

Após alguns meses surge a necessidade de alterar o contrato.

Novo retorno:

```json
{
    "categoryId":"8d1e",
    "description":"Electronics"
}
```

Para novos clientes isso pode parecer uma melhoria.

Para clientes antigos isso representa uma quebra completa de compatibilidade.

Sem versionamento todas as aplicações deixam de funcionar imediatamente.

---

# Estratégia adotada

O Atlas Commerce utiliza **Versionamento por URL (URI Versioning)**.

Todos os endpoints possuem a versão diretamente na URL.

Exemplo:

```
/api/v1/categories
```

```
/api/v1/products
```

```
/api/v1/orders
```

```
/api/v1/users
```

---

# Fluxo da Requisição

```
Cliente

      │

GET /api/v1/categories

      │

Spring Dispatcher

      │

CategoryController

      │

CategoryService

      │

Repository

      │

PostgreSQL
```

A versão faz parte do caminho da requisição e identifica qual contrato será utilizado.

---

# Por que utilizar Versionamento por URL?

Existem diversas estratégias para versionar APIs REST.

No Atlas Commerce foi escolhida a abordagem mais simples, explícita e amplamente adotada pela indústria.

Benefícios:

- Fácil de entender
- Fácil de documentar
- Compatível com Swagger
- Compatível com Cache HTTP
- Fácil integração com API Gateway
- Fácil configuração em Load Balancer

---

# Comparação entre estratégias

| Estratégia | Exemplo | Recomendado |
|------------|----------|-------------|
| URL Versioning | `/api/v1/categories` | ✅ Sim |
| Header Versioning | `X-API-Version:1` | ⚠️ Não |
| Media Type | `Accept: application/vnd.v1+json` | ⚠️ Não |
| Query Parameter | `?version=1` | ❌ Não |

---

# Convenção Oficial

Toda API deverá seguir o padrão:

```
/api/v{versão}/{recurso}
```

Exemplos:

```
/api/v1/categories
```

```
/api/v1/products
```

```
/api/v1/orders
```

```
/api/v1/cart
```

```
/api/v1/payment
```

Nunca criar endpoints fora desse padrão.

---

# Quando criar uma nova versão?

Criar uma nova versão **apenas quando houver Breaking Changes**.

Exemplos:

✔ Alterar estrutura do JSON

✔ Remover um campo existente

✔ Alterar tipo de um atributo

✔ Alterar comportamento incompatível

---

# Quando NÃO criar uma nova versão?

Os seguintes casos não exigem nova versão:

✔ Adicionar novo endpoint

✔ Adicionar novo campo opcional

✔ Melhorar performance

✔ Corrigir bugs internos

✔ Refatoração

✔ Alterações de implementação

---

# Exemplo Prático

Versão atual:

```
GET /api/v1/categories
```

Resposta:

```json
{
    "id":"uuid",
    "name":"Electronics"
}
```

Nova necessidade:

Adicionar descrição.

Resposta:

```json
{
    "id":"uuid",
    "name":"Electronics",
    "description":"Electronic devices"
}
```

Como o novo campo é opcional, a API permanece em **v1**.

---

Agora imagine a remoção do campo "name":

```json
{
    "id":"uuid",
    "description":"Electronic devices"
}
```

Essa alteração quebra clientes existentes.

Nesse caso deve ser criada:

```
/api/v2/categories
```

---

# Evolução da API

```
v1

│

├── Categories

├── Products

├── Orders

│

└──────────────► Tempo

                  │

                  ▼

                 v2
```

As versões coexistem durante o período de migração.

---

# Decisão Arquitetural

Esta estratégia foi definida nas ADRs:

- ADR-000 — Arquitetura do Projeto
- ADR-004 — Repository Pattern
- ADR-005 — Package by Feature

---

# Boas Práticas

✔ Nunca remover endpoints em produção.

✔ Nunca alterar contratos existentes.

✔ Adicionar campos apenas quando compatíveis.

✔ Versionar somente quando necessário.

✔ Documentar todas as mudanças.

✔ Manter versões antigas durante o período de migração.

---

# Erros Comuns

❌ Criar `/api/v2` apenas porque adicionou um endpoint.

❌ Misturar `/v1` e `/v2` no mesmo Controller.

❌ Alterar respostas da versão atual.

❌ Remover endpoints sem período de depreciação.

❌ Criar versões sem documentação.

---

# Referências

- REST API Design Best Practices
- RFC 9110 — HTTP Semantics
- Microsoft REST API Guidelines
- Google API Design Guide
- Spring Boot REST Documentation

---

# Próximo Capítulo

authentication.md

No próximo capítulo será definida toda a estratégia de autenticação, autorização, JWT, filtros de segurança e fluxo completo de login do Atlas Commerce.