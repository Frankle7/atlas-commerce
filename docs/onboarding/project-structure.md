# Estrutura do Projeto

## Objetivo

Apresentar a organização física do Atlas Commerce, explicando a responsabilidade de cada diretório, sua relação com a arquitetura do sistema e as boas práticas adotadas para manter o projeto escalável.

---

# Contexto

Projetos pequenos costumam começar simples.

À medida que novas funcionalidades são adicionadas, a organização do código torna-se um dos fatores mais importantes para manter a produtividade da equipe.

Uma estrutura mal organizada gera:

- arquivos gigantes;
- dependências circulares;
- duplicação de código;
- dificuldade para localizar funcionalidades;
- alto custo de manutenção.

O Atlas Commerce foi planejado para crescer desde o primeiro commit.

Toda a organização do projeto foi desenhada pensando em:

- escalabilidade;
- modularização;
- facilidade de manutenção;
- colaboração entre desenvolvedores.

---

# Visão Geral

```
atlas-commerce
│
├── backend/
│
├── frontend/
│
├── database/
│
├── docker/
│
├── docs/
│
├── infra/
│
├── scripts/
│
├── docker-compose.yml
│
├── README.md
│
└── LICENSE
```

Cada diretório possui uma responsabilidade bem definida.

---

# Diretório Backend

```
backend/
```

Contém toda a aplicação Spring Boot.

Dentro dele ficam:

- regras de negócio
- APIs
- persistência
- autenticação
- configurações
- testes

Estrutura:

```
backend/
    atlas-api/
        src/
            main/
            test/
```

---

# Diretório Frontend

```
frontend/
```

Responsável pela aplicação cliente.

Neste projeto o frontend será desenvolvido posteriormente.

Pode conter aplicações como:

- Flutter
- React
- Angular
- Next.js

---

# Diretório Database

```
database/
```

Armazena toda a documentação relacionada ao banco de dados.

Exemplo:

```
database/

    docs/

    migrations/

    schema/

    seed/
```

---

## docs/

Documentação do domínio do banco.

Exemplos:

- entidades
- relacionamentos
- regras

---

## schema/

Diagramas ER.

Arquivos Draw.io.

Modelagem lógica.

Modelagem física.

---

## migrations/

Scripts SQL utilizados pelo Flyway.

Exemplo:

```
V001__create_category_table.sql
```

---

## seed/

Dados iniciais utilizados durante desenvolvimento.

Exemplo:

- categorias
- usuários
- permissões

---

# Diretório Docker

```
docker/
```

Responsável por todos os containers utilizados pelo projeto.

Exemplo:

```
docker/

    postgres/

    redis/

    nginx/
```

Cada tecnologia possui sua própria configuração.

---

# Diretório Docs

```
docs/
```

É considerado o livro técnico do Atlas Commerce.

Nele ficam todas as decisões arquiteturais do projeto.

Estrutura:

```
docs/

    adr/

    api/

    architecture/

    deployment/

    roadmap/

    onboarding/

    standards/

    contribution/

    missions/
```

Toda alteração relevante no projeto deve refletir na documentação correspondente.

---

# Diretório Infra

```
infra/
```

Contém configurações relacionadas à infraestrutura.

Exemplos:

- Kubernetes
- Terraform
- AWS
- Azure
- GCP

No estágio inicial poderá permanecer vazio.

---

# Diretório Scripts

```
scripts/
```

Armazena scripts utilitários.

Exemplos:

- backup
- restore
- build
- limpeza
- geração automática

---

# Estrutura da Aplicação Spring

Dentro de:

```
backend/

atlas-api/

src/

main/

java/

com/

atlascommerce/
```

Cada domínio possui seu próprio módulo.

```
category/

product/

order/

inventory/

payment/

user/

address/

cart/

notification/
```

Cada módulo é completamente independente.

---

# Organização Interna de um Módulo

Exemplo:

```
category/

controller/

service/

repository/

entity/

dto/

mapper/

validator/

specification/
```

Cada pacote possui apenas uma responsabilidade.

---

## controller

Responsável pelos endpoints REST.

Nunca contém regra de negócio.

Recebe requisições.

Retorna respostas HTTP.

---

## service

Camada responsável pelas regras de negócio.

Toda lógica da aplicação deve estar aqui.

É o coração do sistema.

---

## repository

Responsável pelo acesso ao banco de dados.

Utiliza Spring Data JPA.

Não contém regra de negócio.

---

## entity

Representa as tabelas do banco.

Utiliza anotações JPA.

---

## dto

Objetos utilizados para entrada e saída da API.

Evitam expor entidades diretamente.

---

## mapper

Converte:

DTO → Entity

Entity → DTO

Pode utilizar MapStruct futuramente.

---

## validator

Implementa regras de validação específicas.

Complementa Bean Validation.

---

## specification

Responsável por filtros dinâmicos.

Utiliza Specification do Spring Data.

Permite consultas complexas.

---

# Fluxo Entre Camadas

```
Cliente

↓

Controller

↓

Service

↓

Repository

↓

Banco
```

Cada camada conversa apenas com sua vizinha.

Isso reduz acoplamento.

---

# Organização por Feature

O Atlas Commerce utiliza a estratégia:

Package By Feature.

Ou seja:

```
category/

product/

order/
```

ao invés de:

```
controller/

service/

repository/
```

globais.

Essa decisão facilita a evolução do sistema.

Mais detalhes em:

ADR-005 — Package by Feature.

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

Dependências inversas não são permitidas.

---

# O Que Não Fazer

Não criar classes utilitárias gigantes.

Não compartilhar lógica entre módulos sem necessidade.

Não acessar Repository diretamente pelo Controller.

Não colocar regra de negócio na Entity.

Não utilizar DTO como Entity.

---

# Boas Práticas

Uma classe deve possuir apenas uma responsabilidade.

Um pacote deve representar apenas um contexto.

Evite dependências cruzadas.

Sempre documente mudanças arquiteturais.

Mantenha os módulos independentes.

Prefira composição à herança.

Utilize interfaces para desacoplamento.

---

# Estrutura Esperada Após Algumas Sprints

```
backend/

category/

product/

order/

inventory/

payment/

cart/

user/

auth/

notification/

common/

shared/
```

Cada módulo evolui de forma independente.

Novos módulos podem ser adicionados sem impactar os existentes.

---

# Relação com Outros Documentos

Architecture

Package Architecture

Module Diagram

Database Architecture

Deployment

ADR-000

ADR-005

---

# Referências

Spring Boot Reference

Spring Data JPA

Clean Architecture — Robert C. Martin

Domain Driven Design — Eric Evans

Spring Modulith

---

# Próximo Capítulo

git-workflow.md