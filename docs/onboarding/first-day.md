# First Day

## Objetivo

Apresentar o passo a passo para que um novo desenvolvedor consiga preparar o ambiente, compreender a arquitetura do Atlas Commerce e realizar sua primeira contribuição seguindo os padrões oficiais do projeto.

Ao finalizar este guia, qualquer desenvolvedor deverá ser capaz de:

- clonar o projeto;
- configurar o ambiente local;
- executar a aplicação;
- compreender a estrutura do repositório;
- entender o fluxo de Git;
- criar sua primeira Feature;
- abrir um Pull Request.

---

# Contexto

Todo projeto possui uma curva inicial de aprendizado.

Sem uma documentação adequada, novos integrantes precisam descobrir sozinhos:

- como instalar o projeto;
- quais ferramentas utilizar;
- como funciona a arquitetura;
- onde implementar novas funcionalidades;
- como contribuir corretamente.

Este documento reduz drasticamente esse tempo de adaptação.

---

# Motivação

O Atlas Commerce foi construído para servir também como um projeto de referência em arquitetura de software.

Por isso, cada novo desenvolvedor deve aprender não apenas a executar o sistema, mas também compreender as decisões arquiteturais que sustentam sua evolução.

Nosso objetivo é que qualquer pessoa consiga começar a contribuir no projeto em poucas horas.

---

# Pré-requisitos

Antes de iniciar, verifique se possui as seguintes ferramentas instaladas:

| Ferramenta | Versão Recomendada |
|------------|--------------------|
| Git | 2.40+ |
| Java | 21 |
| Maven | Wrapper incluso |
| Docker | Última versão |
| Docker Compose | Última versão |
| PostgreSQL | Via Docker |
| VS Code ou IntelliJ | Atualizado |

---

# Clonando o Projeto

Clone o repositório oficial.

```bash
git clone https://github.com/Frankle7/atlas-commerce.git
```

Entre na pasta.

```bash
cd atlas-commerce
```

---

# Conhecendo a Estrutura

Antes de executar qualquer comando, conheça a organização do projeto.

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

Toda a documentação oficial está localizada em:

```
docs/
```

Todo desenvolvimento do backend ocorre em:

```
backend/atlas-api
```

---

# Configurando o Ambiente

Copie o arquivo de exemplo das variáveis de ambiente.

```
.env
```

Configure:

- usuário do banco;
- senha;
- porta;
- variáveis da aplicação.

---

# Subindo a Infraestrutura

Execute:

```bash
docker compose up -d
```

Esse comando iniciará:

- PostgreSQL;
- demais serviços definidos no Docker Compose.

Verifique se os containers estão ativos.

```bash
docker ps
```

---

# Executando a Aplicação

Entre na pasta da API.

```bash
cd backend/atlas-api
```

Execute:

```bash
./mvnw spring-boot:run
```

Ou, no Windows:

```bash
mvnw.cmd spring-boot:run
```

---

# Validando a Execução

Abra o navegador.

```
http://localhost:8080
```

Caso a API esteja funcionando, os endpoints poderão ser acessados normalmente.

---

# Explorando a Documentação

Antes de escrever qualquer código, leia os principais documentos.

Ordem recomendada:

```
README.md

↓

ROADMAP

↓

Architecture

↓

ADR

↓

API

↓

Coding Standards

↓

Git Workflow
```

Essa sequência fornece uma visão completa do projeto.

---

# Entendendo a Arquitetura

O Atlas Commerce utiliza arquitetura modular baseada em domínio.

Cada módulo possui sua própria organização interna.

Exemplo:

```
category

controller

service

repository

entity

dto

mapper

validator
```

Todos seguem exatamente o mesmo padrão.

---

# Fluxo Oficial de Desenvolvimento

Todo desenvolvimento segue este fluxo:

```
Main

↓

Sprint

↓

Feature

↓

Commits

↓

Pull Request

↓

Review

↓

Merge
```

Nunca desenvolvemos diretamente na branch Main.

---

# Criando sua Primeira Sprint

Após sincronizar a Main:

```bash
git checkout main

git pull origin main

git checkout -b sprint-001
```

---

# Criando sua Primeira Feature

A Feature sempre nasce da Sprint.

```bash
git checkout sprint-001

git checkout -b feature/missao-004-category-domain
```

---

# Desenvolvendo

Implemente apenas uma Missão por Feature.

Durante o desenvolvimento:

- mantenha commits pequenos;
- siga os padrões de código;
- atualize a documentação quando necessário.

---

# Commits

Utilizamos Conventional Commits.

Exemplos:

```text
feat(category): create entity

feat(category): create repository

docs(api): document category endpoints

test(category): add repository tests
```

Cada commit deve representar apenas uma alteração lógica.

---

# Atualizando a Documentação

Sempre que houver mudanças relevantes:

- atualize a Mission correspondente;
- crie uma ADR, se necessário;
- atualize a documentação da API;
- revise exemplos.

No Atlas Commerce, documentação faz parte da entrega.

---

# Executando Testes

Antes de abrir um Pull Request:

```bash
./mvnw test
```

Todos os testes devem passar.

---

# Abrindo um Pull Request

Ao concluir a Feature:

```
feature/missao-004-category-domain

↓

Pull Request

↓

sprint-001
```

Inclua:

- objetivo;
- descrição;
- alterações realizadas;
- testes executados.

---

# Checklist do Primeiro Dia

Ao finalizar este guia, confirme:

- Projeto clonado.
- Ambiente configurado.
- Docker funcionando.
- Banco iniciado.
- API executando.
- Estrutura compreendida.
- Fluxo Git entendido.
- Primeira Feature criada.
- Primeiro commit realizado.

---

# Boas Práticas

Leia a documentação antes de implementar.

Faça commits pequenos.

Documente decisões importantes.

Utilize nomes claros.

Mantenha o padrão arquitetural.

Atualize as ADRs quando necessário.

Sempre execute testes antes do merge.

---

# Erros Comuns

Criar código sem entender a arquitetura.

Misturar várias funcionalidades na mesma Feature.

Modificar a Main diretamente.

Ignorar a documentação.

Não atualizar a Mission correspondente.

Abrir Pull Request sem testes.

---

# Fluxo Visual

```
Clonar Projeto

↓

Configurar Ambiente

↓

Executar Docker

↓

Executar API

↓

Ler Documentação

↓

Criar Sprint

↓

Criar Feature

↓

Desenvolver

↓

Commit

↓

Testes

↓

Pull Request

↓

Review

↓

Merge
```

---

# Próximos Passos

Após concluir o primeiro dia, recomenda-se estudar os seguintes documentos:

1. `development-environment.md`
2. `git-workflow.md`
3. `architecture/architecture.md`
4. `roadmap/ROADMAP.md`
5. `standards/coding-standards.md`
6. `api/api.md`

Esses capítulos aprofundam o entendimento sobre a arquitetura, os padrões e o fluxo de desenvolvimento do Atlas Commerce.

---

# Relação com Outros Documentos

- README.md
- onboarding/development-environment.md
- onboarding/git-workflow.md
- architecture/architecture.md
- roadmap/ROADMAP.md
- standards/coding-standards.md
- contribution/contribution.md

---

# Referências

- Spring Boot Documentation
- Maven Documentation
- Docker Documentation
- PostgreSQL Documentation
- Conventional Commits
- GitHub Flow

---

# Próximo Capítulo

development-environment.md