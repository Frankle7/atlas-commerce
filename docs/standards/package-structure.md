# Estrutura de Pacotes

---

# Objetivo

Definir o padrão oficial de organização dos pacotes do Atlas Commerce.

Este documento apresenta a arquitetura utilizada pelo projeto, explica por que ela foi escolhida, quais responsabilidades pertencem a cada camada e quais regras devem ser seguidas durante toda a evolução do sistema.

Ao concluir este capítulo, o desenvolvedor deverá ser capaz de criar um novo módulo mantendo exatamente o mesmo padrão utilizado por todo o projeto.

---

# Contexto

Projetos de software normalmente evoluem durante muitos anos.

Novas funcionalidades são adicionadas continuamente, equipes crescem e dezenas de desenvolvedores passam a trabalhar sobre a mesma base de código.

Quando não existe uma arquitetura bem definida, alguns problemas inevitavelmente aparecem:

- Classes gigantes.
- Código duplicado.
- Alto acoplamento.
- Baixa coesão.
- Dependências circulares.
- Dificuldade para localizar arquivos.
- Onboarding demorado para novos desenvolvedores.

A organização do código influencia diretamente a produtividade da equipe.

Por esse motivo, a estrutura dos pacotes foi tratada como uma decisão arquitetural do Atlas Commerce.

---

# O Problema do Package by Layer

A maioria dos projetos Spring Boot inicia utilizando a organização conhecida como **Package by Layer**.

```
controller/
service/
repository/
entity/
dto/
```

À medida que o sistema cresce, todos os Controllers ficam em uma única pasta.

Todos os Services ficam em outra.

Todos os Repositories ficam em outra.

Após alguns meses o projeto passa a possuir centenas de arquivos distribuídos apenas por tecnologia.

Encontrar código torna-se cada vez mais difícil.

Mudanças simples exigem navegar por diversos diretórios diferentes.

A manutenção torna-se lenta.

---

# A Solução Escolhida

O Atlas Commerce adota o padrão **Package by Feature**.

Em vez de organizar o código pela tecnologia utilizada, cada domínio da aplicação possui sua própria estrutura completa.

```
category/

product/

order/

payment/

cart/

inventory/

notification/
```

Cada módulo contém todas as classes necessárias para funcionar de forma independente.

Essa abordagem melhora a organização do projeto, reduz o acoplamento entre módulos e facilita sua evolução.

---

# Comparação entre as abordagens

| Package by Layer | Package by Feature |
|------------------|--------------------|
| Organização por tecnologia | Organização por domínio |
| Controllers centralizados | Controllers separados por módulo |
| Services espalhados | Services agrupados por domínio |
| Difícil localizar código | Fácil localizar código |
| Escala mal | Escala muito bem |
| Alto acoplamento | Baixo acoplamento |

Para projetos pequenos ambas as abordagens funcionam.

Para aplicações grandes, o Package by Feature apresenta vantagens significativas.

---

# Estrutura Oficial

Todos os módulos seguem exatamente a mesma organização.

```
src/main/java/com/atlascommerce

├── category
│   ├── controller
│   ├── dto
│   ├── entity
│   ├── mapper
│   ├── repository
│   ├── service
│   ├── specification
│   └── validator
│
├── product
├── order
├── user
├── payment
├── cart
├── inventory
├── notification
├── auth
├── security
├── shared
├── common
├── config
└── exception
```

Cada domínio possui todas as suas camadas organizadas localmente.

Nenhum módulo depende da estrutura interna de outro módulo.

---

# Responsabilidade de cada pacote

## controller

Responsável por receber requisições HTTP.

Funções:

- Receber Requests.
- Validar entrada.
- Chamar Services.
- Retornar Responses.

Não deve conter regras de negócio.

Fluxo:

```
Cliente

↓

CategoryController

↓

CategoryService
```

---

## dto

Representa os contratos públicos da API.

Existem dois tipos principais:

- Request DTO
- Response DTO

Exemplo:

```
CreateCategoryRequest

UpdateCategoryRequest

CategoryResponse
```

As Entities nunca devem ser expostas diretamente para o cliente.

---

## entity

Representa os objetos persistidos no banco de dados.

As Entities descrevem apenas o estado da aplicação.

Elas não devem conter lógica de apresentação nem regras específicas da API.

Exemplo:

```
Category

Product

Order
```

---

## repository

Responsável pela comunicação com o banco de dados.

Todas as consultas passam por esta camada.

Exemplo:

```
CategoryRepository
extends JpaRepository
```

O Repository não contém regras de negócio.

---

## service

Representa o coração da aplicação.

Nesta camada encontram-se:

- regras comerciais;
- validações de negócio;
- integrações;
- orquestração entre componentes.

Todo comportamento do sistema deve partir da Service.

---

## mapper

Responsável por converter objetos entre diferentes camadas.

Exemplo:

```
Request DTO

↓

Entity

↓

Response DTO
```

Ferramentas recomendadas:

- MapStruct
- Mapper Manual

---

## specification

Contém filtros dinâmicos utilizados pelas consultas.

Exemplo:

```
name contains

status equals

createdAfter

priceBetween
```

Ideal para buscas complexas.

---

## validator

Centraliza validações específicas do domínio.

Exemplos:

- Categoria duplicada.
- Nome inválido.
- Categoria pai inexistente.
- Estado inconsistente.

Separar validações da Service mantém a lógica de negócio limpa e organizada.

---

# Fluxo de Execução

Durante uma requisição HTTP o sistema segue exatamente o fluxo abaixo.

```
Cliente

↓

Controller

↓

Request DTO

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

Mapper

↓

Response DTO

↓

Controller

↓

Cliente
```

Cada camada possui apenas uma responsabilidade.

Esse fluxo deve permanecer consistente em todos os módulos.

---

# Dependências Permitidas

```
Controller

↓

Service

↓

Repository

↓

Banco de Dados
```

As dependências sempre apontam para baixo.

---

# Dependências Proibidas

O projeto estabelece algumas regras importantes.

❌ Controller acessando Repository diretamente.

❌ DTO acessando banco.

❌ Entity conhecendo Controller.

❌ Validator acessando Controller.

❌ Mapper realizando consultas.

Essas restrições reduzem o acoplamento e aumentam a previsibilidade da arquitetura.

---

# Como Criar um Novo Módulo

Sempre que um novo domínio for iniciado, sua estrutura deve ser criada completamente.

Exemplo:

```
coupon/

├── controller
├── dto
├── entity
├── mapper
├── repository
├── service
├── specification
└── validator
```

Mesmo que algumas pastas permaneçam inicialmente vazias.

Isso mantém todos os módulos padronizados.

---

# Evolução da Arquitetura

Hoje o projeto pode conter apenas alguns módulos.

```
Category

Product
```

Com o crescimento da aplicação novos domínios poderão surgir.

```
Order

Coupon

Shipping

Invoice

Marketplace

Seller

Review
```

A estrutura permanecerá exatamente a mesma.

Essa previsibilidade reduz significativamente o custo de manutenção.

---

# Boas Práticas

✔ Organizar por domínio.

✔ Uma responsabilidade por camada.

✔ Controllers pequenos.

✔ Services responsáveis pelas regras.

✔ DTOs específicos.

✔ Repositories simples.

✔ Validators reutilizáveis.

✔ Mappers centralizados.

✔ Baixo acoplamento.

✔ Alta coesão.

---

# Erros Comuns

❌ Colocar regras de negócio em Controllers.

❌ Criar Services gigantes.

❌ Expor Entities na API.

❌ Misturar módulos diferentes.

❌ Criar classes utilitárias para tudo.

❌ Ignorar Validators.

❌ Quebrar o fluxo arquitetural.

---

# Benefícios

A arquitetura adotada oferece diversos benefícios.

- Organização previsível.
- Facilidade para localizar código.
- Escalabilidade.
- Melhor onboarding.
- Facilidade para testes.
- Baixo acoplamento.
- Alta coesão.
- Evolução contínua da aplicação.

Todos os módulos seguem exatamente o mesmo padrão.

---

# Decisão Arquitetural

Este documento implementa as decisões definidas nos seguintes ADRs:

- ADR-000 — Arquitetura Geral.
- ADR-004 — Repository Pattern.
- ADR-005 — Package by Feature.

---

# Referências

- Spring Boot Documentation
- Spring Data JPA
- Domain-Driven Design — Eric Evans
- Clean Architecture — Robert C. Martin
- Package by Feature
- SOLID Principles

---

# Próximo Capítulo

ROADMAP.md