# CI/CD

---

# Objetivo

Definir o processo oficial de Integração Contínua (Continuous Integration) e Entrega Contínua (Continuous Delivery) do Atlas Commerce.

Este documento apresenta como o código evolui desde um commit realizado pelo desenvolvedor até a disponibilização de uma nova versão da aplicação.

Ao concluir este capítulo, o desenvolvedor compreenderá todas as etapas da pipeline de qualidade, automação, validação e publicação do projeto.

---

# Contexto

Projetos modernos não realizam deploy manual.

Todo o processo é automatizado através de pipelines responsáveis por validar o código antes que ele seja integrado à branch principal.

O objetivo da CI/CD é reduzir erros humanos, aumentar a qualidade do software e acelerar a entrega de novas funcionalidades.

---

# Motivação

Imagine uma equipe com dezenas de desenvolvedores realizando alterações simultaneamente.

Sem automação poderiam ocorrer problemas como:

- código quebrado na main;
- deploy de funcionalidades incompletas;
- testes esquecidos;
- conflitos frequentes;
- regressões em produção.

A pipeline garante que apenas código validado seja publicado.

---

# O que é CI

Continuous Integration (Integração Contínua) consiste em integrar pequenas alterações de código frequentemente ao repositório principal.

A cada novo commit, uma série de validações é executada automaticamente.

Exemplo:

```
Commit

↓

Build

↓

Testes

↓

Validações

↓

Merge
```

Caso alguma etapa falhe, o código não deve ser integrado.

---

# O que é CD

Continuous Delivery (Entrega Contínua) consiste em preparar automaticamente uma versão pronta para implantação.

Fluxo:

```
Merge

↓

Build

↓

Package

↓

Deploy

↓

Ambiente
```

Toda versão publicada deve estar pronta para ser disponibilizada em produção.

---

# Pipeline Oficial

O Atlas Commerce utiliza uma pipeline composta pelas seguintes etapas.

```
Developer

↓

Git Commit

↓

GitHub

↓

Pull Request

↓

Code Review

↓

Build

↓

Testes

↓

Quality Check

↓

Merge

↓

Deploy Development

↓

Deploy Staging

↓

Deploy Production
```

Cada etapa possui uma responsabilidade específica.

---

# Fluxo Git

Todo desenvolvimento inicia em uma Feature Branch.

```
main

↓

sprint-001

↓

feature/mission-004-category
```

Após concluir a implementação:

```
Feature

↓

Pull Request

↓

Sprint

↓

Main
```

Nenhum código é enviado diretamente para a Main.

---

# Build

A primeira etapa da pipeline consiste na compilação do projeto.

Exemplo:

```bash
./mvnw clean verify
```

Objetivos:

- compilar;
- validar dependências;
- gerar artefatos.

Caso a compilação falhe, a pipeline é interrompida.

---

# Testes Automatizados

Após o build são executados os testes.

Categorias:

- testes unitários;
- testes de integração;
- testes de API.

Fluxo:

```
Build

↓

Unit Tests

↓

Integration Tests

↓

API Tests
```

Nenhum deploy ocorre com testes falhando.

---

# Qualidade de Código

Após os testes, a qualidade do código é analisada.

Itens verificados:

- cobertura de testes;
- duplicação;
- complexidade;
- vulnerabilidades;
- code smells.

Ferramentas recomendadas:

- SonarQube;
- JaCoCo;
- SpotBugs.

---

# Code Review

Toda alteração deve passar por revisão.

Fluxo:

```
Feature

↓

Pull Request

↓

Reviewer

↓

Aprovação

↓

Merge
```

O objetivo é garantir:

- qualidade;
- padronização;
- compartilhamento de conhecimento.

---

# Merge

Após aprovação:

```
Feature

↓

Sprint

↓

Main
```

Somente código validado pode ser integrado.

---

# Deploy

Após o merge inicia-se o processo de publicação.

```
Main

↓

Build

↓

Imagem Docker

↓

Deploy

↓

Servidor
```

Esse processo será automatizado futuramente.

---

# Artefatos

Ao final da pipeline são gerados artefatos.

Exemplos:

```
JAR

Docker Image

Relatórios

Cobertura

Logs
```

Esses artefatos podem ser utilizados em ambientes posteriores.

---

# Estratégia de Releases

Cada Sprint gera uma nova versão.

Exemplo:

```
Sprint 001

↓

Release 1.0.0

----------------

Sprint 002

↓

Release 1.1.0
```

A evolução segue Semantic Versioning.

---

# Rollback

Caso um deploy apresente problemas:

```
Nova Versão

↓

Erro

↓

Rollback

↓

Versão Anterior
```

Toda implantação deve possuir plano de retorno.

---

# GitHub Actions

No Atlas Commerce a automação será realizada utilizando GitHub Actions.

Exemplo de fluxo:

```
Push

↓

Workflow

↓

Build

↓

Testes

↓

Deploy
```

Os arquivos de workflow ficarão em:

```
.github/

└── workflows/
```

---

# Estrutura da Pipeline

```
Commit

↓

Build

↓

Testes

↓

Lint

↓

Code Review

↓

Merge

↓

Package

↓

Docker Build

↓

Deploy Development

↓

Deploy Staging

↓

Deploy Production
```

Cada etapa depende da anterior.

---

# Falhas na Pipeline

Se qualquer etapa falhar:

```
Pipeline

↓

Erro

↓

Deploy Cancelado
```

Nenhuma versão defeituosa deve avançar para os próximos ambientes.

---

# O que NÃO fazer

Nunca:

- realizar deploy manual em produção;
- ignorar testes falhando;
- aprovar Pull Requests sem revisão;
- realizar merge direto na Main;
- publicar versões sem validação.

---

# Boas Práticas

✔ Commits pequenos.

✔ Pull Requests objetivos.

✔ Pipeline automatizada.

✔ Testes obrigatórios.

✔ Build reproduzível.

✔ Code Review obrigatório.

✔ Deploy automatizado.

✔ Rollback documentado.

✔ Monitoramento após publicação.

---

# Benefícios

A estratégia de CI/CD proporciona:

- maior qualidade;
- entregas frequentes;
- menos erros;
- deploy previsível;
- redução de retrabalho;
- integração contínua;
- maior confiança na publicação.

---

# Relação com Outros Documentos

Este documento complementa:

- deployment.md
- docker.md
- postgres.md
- environments.md
- git-workflow.md
- contribution.md
- code-review.md

---

# Decisão Arquitetural

As práticas descritas neste documento seguem as decisões registradas em:

- ADR-000 — Arquitetura Geral
- ADR-004 — Repository Pattern
- ADR-005 — Package by Feature

---

# Referências

- GitHub Actions Documentation
- Continuous Delivery — Martin Fowler
- Spring Boot Documentation
- Docker Documentation
- Semantic Versioning

---

# Próximo Capítulo

roadmap/ROADMAP.md