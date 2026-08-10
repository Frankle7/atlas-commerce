# Git Workflow

## Objetivo

Definir o fluxo oficial de versionamento utilizado no Atlas Commerce, estabelecendo um padrão único para criação de branches, desenvolvimento de funcionalidades, documentação, revisão de código e integração contínua.

Este documento garante que todos os desenvolvedores trabalhem seguindo o mesmo processo, reduzindo conflitos e facilitando a evolução do projeto.

---

# Contexto

À medida que um projeto cresce, múltiplas pessoas passam a trabalhar simultaneamente em diferentes funcionalidades.

Sem um fluxo de Git bem definido surgem problemas como:

- conflitos frequentes;
- commits desorganizados;
- branches abandonadas;
- dificuldade para localizar alterações;
- histórico pouco confiável;
- merges inseguros.

O Git Workflow do Atlas Commerce foi projetado para manter o histórico limpo, previsível e escalável.

---

# Filosofia

O repositório representa a evolução do produto.

Cada commit deve contar parte dessa história.

Cada branch possui uma responsabilidade.

Cada Sprint possui um objetivo.

Cada Missão representa uma entrega técnica.

Nada é desenvolvido diretamente na branch principal.

---

# Estrutura Oficial de Branches

```
main
│
├── sprint-001
│      │
│      ├── feature/missao-004-category-domain
│      ├── feature/missao-005-category-service
│      ├── feature/missao-006-category-api
│      ├── feature/missao-007-validation
│      ├── feature/missao-008-swagger
│      ├── feature/missao-009-tests
│      └── feature/missao-010-code-review
│
├── sprint-002
│
├── sprint-003
│
└── ...
```

Cada Sprint possui sua própria branch.

Cada Missão possui sua própria Feature Branch.

---

# Fluxo Completo

```
main

↓

Sprint

↓

Feature

↓

Commits

↓

Pull Request

↓

Code Review

↓

Merge para Sprint

↓

Sprint Finalizada

↓

Merge para Main
```

Esse fluxo garante isolamento entre funcionalidades e facilita revisões.

---

# Branch Main

A branch `main` representa a versão oficial do projeto.

Ela deve conter apenas código estável e validado.

Nunca desenvolvemos diretamente na `main`.

A `main` recebe apenas merges de Sprints concluídas.

---

# Branch Sprint

Cada Sprint possui uma branch exclusiva.

Exemplo:

```
sprint-001

sprint-002

sprint-003
```

A Sprint agrupa todas as funcionalidades planejadas para aquele ciclo de desenvolvimento.

Durante a Sprint, novas Features são criadas a partir dela.

---

# Feature Branch

Cada funcionalidade nasce em uma Feature.

Exemplo:

```
feature/missao-004-category-domain

feature/missao-005-category-service

feature/missao-006-category-api
```

A Feature existe apenas durante o desenvolvimento daquela missão.

Após o merge, ela pode ser removida.

---

# Fluxo de Criação

Criando uma Sprint:

```bash
git checkout main

git pull origin main

git checkout -b sprint-001
```

---

Criando uma Feature:

```bash
git checkout sprint-001

git pull

git checkout -b feature/missao-004-category-domain
```

---

# Fluxo de Desenvolvimento

Durante o desenvolvimento:

```
Feature

↓

Commit

↓

Commit

↓

Commit

↓

Pull Request
```

Os commits devem ser pequenos e representar uma única alteração.

---

# Commits

O Atlas Commerce utiliza Conventional Commits.

Exemplos:

```
feat(category): create category entity

feat(category): create repository

feat(category): create service

fix(category): validate duplicate names

docs(api): document category endpoints

test(category): add repository tests
```

Nunca misture múltiplas responsabilidades em um único commit.

---

# Organização dos Commits

Uma Feature pode possuir vários commits.

Exemplo:

```
feat(category): create entity

feat(category): create migration

feat(category): create repository

docs(adr): define category architecture

docs(mission): update mission 004
```

Cada commit representa um passo da evolução da funcionalidade.

---

# Pull Request

Após concluir a Feature:

```
feature/missao-004

↓

Pull Request

↓

sprint-001
```

O Pull Request deve conter:

- descrição da alteração;
- objetivo da missão;
- impacto da mudança;
- checklist de validação.

---

# Checklist de Pull Request

Antes de abrir um PR confirme:

- código compila;
- testes executam;
- documentação atualizada;
- ADR atualizada quando necessário;
- Mission atualizada;
- sem conflitos;
- padrão de código respeitado.

---

# Code Review

Toda Feature passa por revisão.

Durante a revisão verificamos:

- arquitetura;
- legibilidade;
- performance;
- segurança;
- organização;
- testes;
- documentação.

A revisão faz parte do desenvolvimento.

---

# Merge para Sprint

Após aprovação:

```
feature/missao-004

↓

merge

↓

sprint-001
```

A Sprint passa a conter a funcionalidade concluída.

---

# Finalização da Sprint

Quando todas as Missões forem concluídas:

```
feature

↓

Sprint

↓

Main
```

O merge para a `main` representa uma entrega oficial do projeto.

---

# Estrutura de Desenvolvimento

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

Merge Sprint

↓

Merge Main
```

---

# Organização das Missões

Exemplo da Sprint 001:

```
Sprint-001

├── Missão 004
├── Missão 005
├── Missão 006
├── Missão 007
├── Missão 008
├── Missão 009
└── Missão 010
```

Cada missão possui:

- Feature própria;
- documentação própria;
- ADR quando necessário;
- commits independentes.

---

# Fluxo da Documentação

A documentação evolui junto com o código.

Exemplo:

```
Nova arquitetura

↓

Nova ADR

↓

Nova Mission

↓

Implementação

↓

Merge
```

Nunca implementamos primeiro e documentamos depois.

Código e documentação evoluem juntos.

---

# Convenções de Branches

Sprint:

```
sprint-001
```

Feature:

```
feature/missao-004-category-domain
```

Hotfix:

```
hotfix/login-error
```

Bugfix:

```
bugfix/category-validation
```

Release:

```
release/v1.0.0
```

---

# Boas Práticas

Sempre atualizar a Sprint antes de criar uma Feature.

Criar uma Feature para cada Missão.

Realizar commits pequenos.

Escrever mensagens claras.

Atualizar documentação durante o desenvolvimento.

Excluir Features após o merge.

Nunca trabalhar diretamente na Main.

Nunca misturar funcionalidades diferentes na mesma Feature.

---

# Erros Comuns

Criar uma Feature a partir da Main quando deveria partir da Sprint.

Misturar várias Missões na mesma Branch.

Realizar commits gigantes.

Esquecer de atualizar a documentação.

Abrir Pull Request sem testes.

Ignorar Code Review.

---

# Fluxo Resumido

```
Main

↓

Sprint

↓

Feature

↓

Commit

↓

Commit

↓

Pull Request

↓

Review

↓

Merge Sprint

↓

Merge Main
```

---

# Relação com Outros Documentos

- onboarding/first-day.md
- onboarding/development-environment.md
- standards/commit-convention.md
- contribution/contribution.md
- contribution/code-review.md
- roadmap/ROADMAP.md

---

# Referências

- Git Documentation
- GitHub Flow
- Git Flow
- Conventional Commits
- Semantic Versioning

---

# Próximo Capítulo

first-day.md