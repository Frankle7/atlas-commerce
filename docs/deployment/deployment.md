# Deployment

---

# Objetivo

Definir o processo oficial de implantação (Deployment) do Atlas Commerce.

Este documento estabelece como preparar o ambiente, iniciar a infraestrutura, executar a aplicação, validar o funcionamento e disponibilizar novas versões do sistema.

Ao concluir este capítulo, o desenvolvedor será capaz de executar o projeto localmente e compreender como será realizado o deploy em ambientes de homologação e produção.

---

# Contexto

O Atlas Commerce foi desenvolvido seguindo uma arquitetura moderna baseada em containers.

Toda a infraestrutura necessária para executar o projeto pode ser reproduzida utilizando Docker.

Essa abordagem garante que todos os desenvolvedores trabalhem exatamente no mesmo ambiente, reduzindo problemas de configuração e diferenças entre sistemas operacionais.

---

# Motivação

Sem um processo de deployment padronizado surgem diversos problemas:

- ambientes inconsistentes;
- erros difíceis de reproduzir;
- dependências incompatíveis;
- configurações manuais;
- dificuldade para onboarding.

Por esse motivo todo o ambiente do Atlas Commerce é definido como código.

---

# Arquitetura do Ambiente

O ambiente local é composto pelos seguintes serviços.

```
                Atlas Commerce

                       │

          ┌────────────┴────────────┐

          │                         │

     Spring Boot API          PostgreSQL

          │                         │

          └────────────┬────────────┘

                       │

                  Docker Compose
```

Toda a infraestrutura é inicializada através do Docker Compose.

---

# Componentes

## Spring Boot

Responsável pela API REST.

Funções:

- regras de negócio;
- autenticação;
- integração com banco;
- documentação Swagger;
- validações.

---

## PostgreSQL

Banco de dados oficial do projeto.

Responsável por armazenar:

- usuários;
- produtos;
- categorias;
- pedidos;
- pagamentos;
- estoque.

---

## Docker

Padroniza todo o ambiente.

Cada serviço é executado em um container independente.

Benefícios:

- isolamento;
- portabilidade;
- facilidade de configuração;
- reprodutibilidade.

---

## Docker Compose

Responsável por orquestrar todos os containers.

Permite iniciar todo o ambiente utilizando apenas um comando.

---

# Estrutura de Infraestrutura

```
atlas-commerce

docker/

└── postgres/
    ├── Dockerfile
    ├── postgres.conf
    └── init/

docker-compose.yml

.env
```

Toda configuração da infraestrutura encontra-se nesses arquivos.

---

# Pré-requisitos

Antes de iniciar o projeto é necessário possuir:

- Git;
- Docker Desktop;
- Docker Compose;
- Java 21;
- Maven;
- IDE compatível (IntelliJ IDEA ou VS Code).

Verifique as versões instaladas.

```
git --version

docker --version

docker compose version

java --version

mvn --version
```

---

# Configuração do Ambiente

Clone o repositório.

```bash
git clone https://github.com/seu-usuario/atlas-commerce.git

cd atlas-commerce
```

Configure as variáveis de ambiente.

Arquivo:

```
.env
```

Exemplo:

```env
POSTGRES_DB=atlas

POSTGRES_USER=atlas

POSTGRES_PASSWORD=atlas123

SPRING_PROFILES_ACTIVE=local
```

Nunca versionar credenciais reais.

---

# Inicializando o Banco

Suba o PostgreSQL utilizando Docker.

```bash
docker compose up -d
```

Verifique os containers.

```bash
docker ps
```

Resultado esperado:

```
atlas-postgres

Running
```

---

# Executando a API

Entre na pasta da aplicação.

```bash
cd backend/atlas-api
```

Execute.

```bash
./mvnw spring-boot:run
```

Ou:

```bash
mvn spring-boot:run
```

Resultado esperado.

```
Started AtlasApiApplication
```

---

# Validando a Aplicação

Após iniciar a API, valide os principais endpoints.

Health Check.

```
GET

http://localhost:8080/actuator/health
```

Swagger.

```
http://localhost:8080/swagger-ui/index.html
```

API Base.

```
http://localhost:8080/api/v1
```

A aplicação deve responder corretamente antes de prosseguir com o desenvolvimento.

---

# Fluxo Completo de Inicialização

```
Clone

↓

Configurar .env

↓

Docker Compose

↓

PostgreSQL

↓

Spring Boot

↓

Flyway

↓

Aplicação Inicializada

↓

Swagger

↓

Desenvolvimento
```

Este é o fluxo padrão utilizado por todos os desenvolvedores.

---

# Migrations

O Atlas Commerce utiliza Flyway para controle de versão do banco de dados.

Todas as alterações estruturais devem ser realizadas através de migrations.

Estrutura:

```
src/main/resources/db/migration

V001__create_category_table.sql

V002__create_product_table.sql

V003__create_order_table.sql
```

Nunca modificar migrations já executadas.

Sempre criar uma nova versão.

---

# Ambientes

O projeto prevê diferentes ambientes de execução.

```
Local

↓

Development

↓

Homologation

↓

Production
```

Cada ambiente possui configurações próprias.

---

# Variáveis de Ambiente

As configurações devem ser externas ao código.

Exemplos.

```
DATABASE_URL

DATABASE_USERNAME

DATABASE_PASSWORD

JWT_SECRET

SERVER_PORT

SPRING_PROFILES_ACTIVE
```

Nunca armazenar segredos diretamente no repositório.

---

# Processo de Release

Quando uma Sprint for concluída, o fluxo oficial será:

```
Feature

↓

Sprint

↓

Main

↓

Tag

↓

Build

↓

Deploy

↓

Produção
```

Cada release representa uma versão estável do sistema.

---

# Versionamento

O Atlas Commerce utiliza Semantic Versioning.

Formato:

```
MAJOR.MINOR.PATCH
```

Exemplos.

```
1.0.0

1.1.0

1.1.1

2.0.0
```

---

# Logs

Durante a execução acompanhe os logs da aplicação.

Docker.

```bash
docker logs atlas-postgres
```

Spring Boot.

```bash
mvn spring-boot:run
```

Os logs auxiliam na identificação de erros durante a inicialização.

---

# Solução de Problemas

Problema:

```
Port already in use
```

Solução:

Finalizar o processo utilizando a porta ou alterar a configuração da aplicação.

---

Problema:

```
Database connection refused
```

Verificar:

- container iniciado;
- credenciais;
- porta;
- arquivo `.env`.

---

Problema:

```
Flyway Migration Failed
```

Verificar:

- ordem das migrations;
- sintaxe SQL;
- versão do banco.

---

# O que NÃO fazer

Nunca:

- executar a aplicação sem banco de dados;
- alterar migrations executadas;
- versionar senhas;
- modificar configurações diretamente em produção;
- executar deploy manual sem validação.

---

# Boas Práticas

✔ Utilizar Docker para todos os ambientes locais.

✔ Manter variáveis no `.env`.

✔ Versionar apenas arquivos de configuração.

✔ Criar uma migration para cada alteração estrutural.

✔ Validar a aplicação antes de realizar commits.

✔ Monitorar logs durante a inicialização.

✔ Automatizar processos de deploy sempre que possível.

---

# Benefícios

Este processo proporciona:

- ambiente padronizado;
- onboarding simplificado;
- infraestrutura reproduzível;
- menor incidência de erros;
- facilidade para manutenção;
- deploy previsível;
- escalabilidade futura.

---

# Relação com Outros Documentos

Este documento complementa:

- docker.md
- postgres.md
- environments.md
- ci-cd.md
- development-environment.md
- ROADMAP.md

---

# Decisão Arquitetural

Este processo está alinhado com:

- ADR-000 — Arquitetura Geral
- ADR-001 — PostgreSQL
- ADR-004 — Repository Pattern

---

# Referências

- Spring Boot Documentation
- Docker Documentation
- Docker Compose Documentation
- PostgreSQL Documentation
- Flyway Documentation
- Semantic Versioning

---

# Próximo Capítulo

deployment/docker.md