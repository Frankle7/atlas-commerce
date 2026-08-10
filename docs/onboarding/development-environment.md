# Development Environment

## Objetivo

Definir o ambiente oficial de desenvolvimento utilizado pelo Atlas Commerce, garantindo que todos os desenvolvedores trabalhem utilizando as mesmas ferramentas, versões e configurações.

Este documento funciona como o manual de preparação do ambiente de desenvolvimento e serve como referência para novas instalações, manutenção e padronização da equipe.

---

# Contexto

Um dos maiores problemas em projetos de software é a inconsistência entre ambientes.

Diferenças de versões de Java, Maven, Docker ou PostgreSQL podem gerar erros difíceis de reproduzir, comprometendo a produtividade da equipe.

O Atlas Commerce adota um ambiente totalmente padronizado para eliminar esse tipo de problema.

---

# Motivação

Um ambiente de desenvolvimento consistente oferece diversos benefícios:

- reduz problemas de compatibilidade;
- facilita o onboarding de novos desenvolvedores;
- garante que todos utilizem as mesmas versões das ferramentas;
- melhora a previsibilidade dos builds;
- simplifica a configuração de ambientes locais.

Nosso objetivo é que qualquer desenvolvedor consiga preparar o ambiente completo em menos de 30 minutos.

---

# Ambiente Oficial

| Ferramenta | Versão Recomendada |
|------------|--------------------|
| Java | 21 LTS |
| Maven | Wrapper (mvnw) |
| Spring Boot | 3.x |
| PostgreSQL | 16+ |
| Docker | Última versão |
| Docker Compose | Última versão |
| Git | 2.40+ |
| VS Code / IntelliJ IDEA | Atualizado |

---

# Estrutura do Projeto

```
atlas-commerce/

backend/
frontend/
database/
docker/
docs/
infra/
scripts/
```

Cada diretório possui uma responsabilidade específica.

---

# Backend

Toda a aplicação Spring Boot está localizada em:

```
backend/atlas-api
```

Estrutura principal:

```
src/

main/

java/

resources/

test/
```

---

# Banco de Dados

O banco oficial do projeto é o PostgreSQL.

Toda a infraestrutura do banco é executada via Docker.

```
docker/

postgres/

init/
```

As migrations ficam em:

```
src/main/resources/db/migration
```

Utilizamos Flyway para controle de versão do banco de dados.

---

# Docker

Toda a infraestrutura é inicializada utilizando Docker Compose.

Executar:

```bash
docker compose up -d
```

Verificar containers:

```bash
docker ps
```

Encerrar ambiente:

```bash
docker compose down
```

---

# Configuração do Ambiente

Na raiz do projeto existe o arquivo:

```
.env
```

Ele concentra variáveis utilizadas pelo ambiente local.

Exemplo:

```env
POSTGRES_DB=atlas
POSTGRES_USER=postgres
POSTGRES_PASSWORD=postgres
SPRING_PROFILES_ACTIVE=local
```

Nunca envie arquivos contendo informações sensíveis para o repositório.

---

# Executando a API

Entre na pasta do backend.

```bash
cd backend/atlas-api
```

Inicie a aplicação.

Linux/macOS:

```bash
./mvnw spring-boot:run
```

Windows:

```bash
mvnw.cmd spring-boot:run
```

---

# Executando Testes

Todos os testes devem ser executados antes de abrir um Pull Request.

```bash
./mvnw test
```

Para limpar o projeto:

```bash
./mvnw clean
```

Compilar:

```bash
./mvnw package
```

---

# Configuração do Git

Verifique sua configuração:

```bash
git config --global user.name

git config --global user.email
```

Caso necessário:

```bash
git config --global user.name "Seu Nome"

git config --global user.email "email@exemplo.com"
```

---

# Estrutura de Branches

O Atlas Commerce utiliza o seguinte fluxo:

```
main

↓

Sprint

↓

Feature

↓

Pull Request

↓

Merge
```

Cada funcionalidade nasce em uma Feature específica.

---

# Configuração da IDE

## VS Code

Extensões recomendadas:

- Extension Pack for Java
- Spring Boot Extension Pack
- Docker
- GitLens
- EditorConfig
- Markdown All in One
- Draw.io Integration
- YAML
- Error Lens
- SonarLint

Arquivo:

```
.vscode/settings.json
```

contém configurações compartilhadas entre todos os desenvolvedores.

---

## IntelliJ IDEA

Plugins recomendados:

- Lombok
- Docker
- Database Tools
- Git
- SonarLint
- Markdown
- PlantUML

---

# Organização dos Pacotes

Cada módulo segue exatamente a mesma estrutura.

```
category/

controller

dto

entity

mapper

repository

service

validator

specification
```

Essa padronização facilita a navegação e reduz a curva de aprendizado.

---

# Convenções de Código

Todo código deve seguir os padrões definidos em:

```
docs/standards/
```

Principais documentos:

- coding-standards.md
- clean-code.md
- naming.md
- package-structure.md

---

# Documentação

Toda decisão arquitetural deve ser registrada.

```
docs/

adr/

missions/

architecture/

api/

roadmap/
```

Documentação é parte integrante da entrega.

---

# Banco de Dados

O banco é controlado por migrations.

Nunca altere tabelas manualmente.

Toda mudança estrutural deve ser realizada através de um novo arquivo de migration.

Exemplo:

```
V001__create_category_table.sql

V002__create_product_table.sql
```

---

# Build do Projeto

Compilar:

```bash
./mvnw clean package
```

Executar testes:

```bash
./mvnw test
```

Gerar artefato:

```bash
./mvnw package
```

---

# Estrutura Recomendada da Máquina

```
SSD

16 GB RAM

Java 21

Docker Desktop

Git

VS Code ou IntelliJ
```

Embora seja possível utilizar configurações inferiores, esse ambiente proporciona melhor desempenho durante o desenvolvimento.

---

# Checklist do Ambiente

Antes de iniciar qualquer missão, confirme:

- Git instalado.
- Java configurado.
- Maven Wrapper funcionando.
- Docker iniciado.
- PostgreSQL executando.
- Projeto compilando.
- Testes executando.
- Variáveis de ambiente configuradas.
- IDE preparada.

---

# Boas Práticas

- Utilize sempre o Maven Wrapper (`mvnw`).
- Nunca altere diretamente o banco de dados.
- Mantenha o Docker atualizado.
- Atualize dependências de forma controlada.
- Utilize o mesmo padrão de IDE e plugins recomendado.
- Execute testes antes de cada commit.

---

# Erros Comuns

- Utilizar versão incorreta do Java.
- Esquecer de iniciar o Docker.
- Executar a aplicação sem configurar o `.env`.
- Alterar tabelas manualmente.
- Ignorar falhas de testes.
- Não sincronizar a branch antes de iniciar uma Feature.

---

# Fluxo do Ambiente

```
Instalar Ferramentas

↓

Clonar Projeto

↓

Configurar .env

↓

Subir Docker

↓

Executar PostgreSQL

↓

Executar Spring Boot

↓

Executar Testes

↓

Iniciar Desenvolvimento
```

---

# Relação com Outros Documentos

- onboarding/first-day.md
- onboarding/git-workflow.md
- onboarding/project-structure.md
- deployment/docker.md
- deployment/postgres.md
- standards/coding-standards.md
- architecture/architecture.md

---

# Referências

- Spring Boot Documentation
- Maven Documentation
- Docker Documentation
- PostgreSQL Documentation
- Flyway Documentation
- Git Documentation

---

# Próximo Capítulo

standards/coding-standards.md