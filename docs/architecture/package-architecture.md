# Arquitetura de Pacotes

# Objetivo

Explicar a organização interna do código-fonte do Atlas Commerce, definindo a responsabilidade de cada pacote, suas dependências, boas práticas e regras de utilização.

Este documento estabelece um padrão único para toda a equipe, garantindo consistência durante o desenvolvimento e facilitando a manutenção do projeto.

---

# Contexto

À medida que um sistema cresce, a organização do código torna-se tão importante quanto a implementação das funcionalidades.

Projetos sem uma estrutura definida tendem a apresentar:

- classes muito grandes
- dependências circulares
- duplicação de código
- baixo reaproveitamento
- dificuldade de manutenção

Para evitar esses problemas, o Atlas Commerce adota a organização **Package by Feature**, onde cada domínio possui todos os componentes necessários para sua implementação.

---

# Motivação

A principal motivação dessa arquitetura é aumentar a coesão dos módulos e reduzir o acoplamento entre funcionalidades.

Cada domínio possui sua própria estrutura interna, permitindo que seja desenvolvido, testado e evoluído de forma independente.

Essa abordagem facilita:

- manutenção
- testes
- escalabilidade
- reutilização
- leitura do código

---

# Organização Geral

Cada domínio do sistema possui a seguinte estrutura:

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

A mesma organização será utilizada para:

```
product

order

user

payment

inventory

cart

address

notification

authentication
```

Todos os módulos seguem exatamente o mesmo padrão.

---

# Controller

## Responsabilidade

Receber requisições HTTP e devolver respostas ao cliente.

O Controller representa a camada de entrada da aplicação.

Suas responsabilidades são:

- receber parâmetros
- validar entrada
- chamar Services
- devolver ResponseEntity

O Controller **não implementa regras de negócio**.

---

## Pode fazer

- receber RequestBody
- receber PathVariable
- receber RequestParam
- chamar Services
- retornar DTOs

---

## Não pode fazer

- acessar Repository
- implementar regras de negócio
- montar consultas SQL
- manipular entidades diretamente

---

## Exemplo

```
GET /api/v1/categories

↓

CategoryController

↓

CategoryService
```

---

# Service

## Responsabilidade

Implementar toda a lógica de negócio da aplicação.

É a camada mais importante do sistema.

Toda regra deve ficar aqui.

Exemplos:

- validar duplicidade
- aplicar regras comerciais
- realizar cálculos
- controlar transações
- orquestrar chamadas

---

## Pode fazer

- utilizar Repository
- utilizar Mapper
- utilizar Validator
- lançar exceções
- iniciar transações

---

## Não pode fazer

- responder HTTP
- acessar RequestBody
- conhecer detalhes da API REST

---

# Repository

## Responsabilidade

Persistir informações no banco de dados.

O Repository representa a camada de acesso aos dados.

Utiliza Spring Data JPA.

---

## Pode fazer

- save()

- findById()

- delete()

- consultas customizadas

---

## Não pode fazer

- implementar regra de negócio
- validar dados
- chamar Services

---

# Entity

## Responsabilidade

Representar tabelas do banco de dados.

As Entities descrevem como os dados são persistidos.

Exemplo:

```
Category

↓

categories
```

As Entities não representam a API.

Elas representam exclusivamente a persistência.

---

# DTO

## Responsabilidade

Transportar dados entre cliente e servidor.

DTO significa:

Data Transfer Object.

Separar DTO da Entity evita:

- exposição do banco
- acoplamento
- quebra de contrato

Exemplo:

```
CategoryRequest

CategoryResponse
```

---

# Mapper

## Responsabilidade

Converter objetos entre diferentes camadas.

Exemplo:

```
CategoryRequest

↓

Category

↓

CategoryResponse
```

A conversão deve ficar centralizada.

Nunca espalhada pelo projeto.

---

# Validator

## Responsabilidade

Centralizar validações específicas do domínio.

Exemplos:

- categoria duplicada
- nome inválido
- regra de negócio

Validações simples podem utilizar Bean Validation.

Validações complexas pertencem ao Validator.

---

# Specification

## Responsabilidade

Construção de consultas dinâmicas.

Permite criar filtros reutilizáveis utilizando JPA Specifications.

Exemplo:

```
Nome

Status

Data

Categoria

Ordenação
```

Tudo sem escrever SQL manualmente.

---

# Dependências Permitidas

```
Controller

↓

Service

↓

Repository

↓

Database
```

Também:

```
Service

↓

Mapper

↓

DTO
```

---

# Dependências Proibidas

Nunca:

```
Controller

↓

Repository
```

Nunca:

```
Repository

↓

Service
```

Nunca:

```
Entity

↓

Controller
```

Nunca:

```
DTO

↓

Repository
```

Cada camada deve conhecer apenas as camadas inferiores.

---

# Fluxo Entre os Pacotes

```
Controller

↓

DTO Request

↓

Service

↓

Validator

↓

Repository

↓

Database

↓

Repository

↓

Mapper

↓

DTO Response

↓

Controller
```

---

# Convenções

Cada módulo deve possuir exatamente a mesma estrutura.

Exemplo:

```
category

product

order

payment

inventory

user
```

Isso facilita:

- localização de arquivos
- onboarding
- manutenção
- padronização

---

# Boas Práticas

- Um Controller por recurso.
- Um Service por domínio.
- Um Repository por Entity.
- Nunca compartilhar lógica entre Controllers.
- Utilizar DTOs para comunicação.
- Utilizar Mapper para conversão.
- Centralizar validações.
- Evitar dependências circulares.

---

# Erros Comuns

Criar Services gigantes.

Colocar regras de negócio no Controller.

Utilizar Entity como resposta da API.

Duplicar validações.

Misturar responsabilidades entre camadas.

Acessar Repository diretamente pelo Controller.

---

# Decisão Arquitetural

Este documento implementa as decisões definidas em:

- ADR-000 — Arquitetura Geral
- ADR-004 — Repository Pattern
- ADR-005 — Package by Feature

---

# Referências

Spring Boot Reference

Spring Data JPA

Clean Architecture — Robert C. Martin

Domain Driven Design — Eric Evans

SOLID Principles

---

# Próximo Capítulo

request-flow.md