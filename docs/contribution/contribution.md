# Contribuição para o Atlas Commerce

---

# Objetivo

Definir o processo oficial de contribuição utilizado no Atlas Commerce.

Este documento estabelece como novos desenvolvimentos devem ser planejados, implementados, revisados e integrados ao projeto, garantindo organização, rastreabilidade e evolução sustentável da plataforma.

Ao concluir este capítulo, o desenvolvedor compreenderá todo o fluxo de trabalho adotado pela equipe, desde a criação de uma Feature até sua entrega na branch principal.

---

# Contexto

Projetos de software crescem continuamente.

Novos módulos são desenvolvidos.

Bugs são corrigidos.

Funcionalidades evoluem.

Sem um processo de contribuição bem definido, rapidamente surgem problemas como:

- conflitos frequentes;
- histórico Git confuso;
- código sem padrão;
- dificuldade para revisar alterações;
- perda de rastreabilidade.

Para evitar esses problemas, o Atlas Commerce adota um fluxo baseado em Sprints, Features, Pull Requests e Code Review.

---

# Motivação

O processo de contribuição foi criado para garantir:

- organização do desenvolvimento;
- histórico Git limpo;
- facilidade para revisar alterações;
- rastreabilidade completa das entregas;
- colaboração entre desenvolvedores;
- evolução previsível da arquitetura.

Todo desenvolvimento deve seguir exatamente este fluxo.

---

# Fluxo Oficial de Desenvolvimento

```
main

↓

Sprint

↓

Feature

↓

Commits

↓

Push

↓

Pull Request

↓

Code Review

↓

Merge na Sprint

↓

Release

↓

main
```

Cada etapa possui responsabilidades específicas.

---

# Estrutura das Branches

O Atlas Commerce utiliza três níveis principais de branches.

```
main

↓

sprint-001

↓

feature/missao-004
```

A branch **main** representa a versão estável do projeto.

As branches **Sprint** agrupam todas as funcionalidades planejadas para um ciclo de desenvolvimento.

As branches **Feature** concentram a implementação de uma única missão.

---

# Branch Principal

A branch `main` deve conter apenas código estável.

Ela representa sempre a versão pronta para produção.

Nunca desenvolva diretamente na main.

---

# Branch de Sprint

Cada Sprint possui sua própria branch.

Exemplo:

```
sprint-001

sprint-002

sprint-003
```

Todas as Features daquela Sprint serão integradas nela antes de chegar à main.

---

# Branch de Feature

Cada missão gera uma Feature específica.

Exemplos:

```
feature/missao-004

feature/missao-005

feature/missao-006
```

Cada Feature possui apenas um objetivo.

Não misture diferentes funcionalidades na mesma branch.

---

# Organização das Missões

As missões iniciais fazem parte do Pré-Projeto.

```
MISSION-001

Planejamento

MISSION-002

Arquitetura

MISSION-003

Setup
```

Essas missões permanecem diretamente na branch main.

A partir da Missão 004 inicia-se o desenvolvimento por Sprint.

---

# Estrutura Geral

```
Pré Projeto

↓

main

├── MISSION-001
├── MISSION-002
├── MISSION-003

↓

Sprint-001

├── MISSION-004
├── MISSION-005
├── MISSION-006
├── MISSION-007
├── MISSION-008
├── MISSION-009
└── MISSION-010
```

---

# Fluxo para Nova Feature

Sempre siga os passos abaixo.

```
Atualizar Sprint

↓

Criar Feature

↓

Implementar

↓

Commitar

↓

Push

↓

Pull Request

↓

Review

↓

Merge
```

---

# Criando uma Nova Feature

A Feature deve nascer sempre da Sprint.

Exemplo:

```bash
git checkout sprint-001

git pull

git checkout -b feature/missao-004
```

Nunca crie uma Feature diretamente da main.

---

# Commits

Todos os commits seguem o padrão Conventional Commits.

Exemplos:

```text
feat(category): create category entity

feat(category): implement category service

fix(category): validate duplicated name

docs(api): update pagination documentation

refactor(service): simplify validation flow

test(category): add repository tests
```

Cada commit deve representar apenas uma alteração lógica.

---

# Pull Request

Ao finalizar a Feature:

```bash
git push origin feature/missao-004
```

Depois abrir um Pull Request para:

```
feature/missao-004

↓

sprint-001
```

Nunca abrir PR diretamente para a main.

---

# Processo de Revisão

Todo Pull Request deve passar por Code Review.

Durante a revisão são avaliados:

- arquitetura;
- qualidade do código;
- aderência aos padrões;
- documentação;
- testes;
- impacto da alteração.

Somente após aprovação o merge poderá ser realizado.

---

# Merge da Sprint

Após todas as missões da Sprint serem concluídas:

```
feature/missao-004

↓

feature/missao-005

↓

feature/missao-006

↓

...

↓

sprint-001
```

A Sprint concentra todas as entregas daquele ciclo.

---

# Release

Quando todas as missões da Sprint forem aprovadas:

```
sprint-001

↓

main
```

Este merge representa uma nova entrega oficial do projeto.

---

# Documentação Obrigatória

Sempre que necessário, atualizar:

- Missões;
- ADRs;
- API;
- Arquitetura;
- Roadmap;
- Padrões;
- Deployment.

Código e documentação evoluem juntos.

---

# Checklist Antes do Push

Antes de enviar uma Feature, confirme:

- código compila;
- testes executam;
- documentação atualizada;
- sem arquivos temporários;
- sem código comentado;
- commits organizados;
- nomes padronizados.

---

# O que NÃO fazer

Nunca:

- desenvolver na main;
- misturar duas missões na mesma Feature;
- criar commits gigantes;
- ignorar Code Review;
- fazer merge sem aprovação;
- alterar histórico compartilhado.

---

# Boas Práticas

✔ Uma missão por Feature.

✔ Uma Sprint por ciclo.

✔ Pequenos commits.

✔ Commits descritivos.

✔ Documentação atualizada.

✔ Pull Requests pequenos.

✔ Revisões frequentes.

✔ Arquitetura consistente.

✔ Código limpo.

---

# Benefícios

Seguindo este fluxo, o Atlas Commerce garante:

- histórico Git organizado;
- rastreabilidade completa;
- releases previsíveis;
- facilidade de manutenção;
- colaboração eficiente;
- evolução segura da arquitetura.

---

# Relação com os Documentos

Este processo complementa os seguintes capítulos:

- git-workflow.md
- commit-convention.md
- code-review.md
- ROADMAP.md
- MILESTONE-01.md

Todos esses documentos trabalham juntos para definir o processo oficial de desenvolvimento do Atlas Commerce.

---

# Decisão Arquitetural

Este fluxo está alinhado com:

- ADR-000 — Arquitetura Geral
- ADR-004 — Repository Pattern
- ADR-005 — Package by Feature

---

# Referências

- Git Documentation
- GitHub Flow
- Git Flow
- Conventional Commits
- Clean Architecture
- Domain-Driven Design

---

# Próximo Capítulo

contribution/pull-request-template.md