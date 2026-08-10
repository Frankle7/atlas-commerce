# Releases

---

# Objetivo

Definir a estratégia oficial de versionamento e publicação do Atlas Commerce.

Este documento apresenta como novas versões são planejadas, identificadas, construídas, documentadas e disponibilizadas aos usuários.

Ao concluir este capítulo, o desenvolvedor compreenderá:

- como uma Release é criada;
- quando uma versão deve ser publicada;
- como utilizar Semantic Versioning;
- quais artefatos acompanham cada Release;
- como manter a rastreabilidade entre código, documentação e roadmap.

---

# Contexto

Todo software evolui continuamente.

Novas funcionalidades são adicionadas.

Bugs são corrigidos.

Arquiteturas evoluem.

Documentações são atualizadas.

Sem um processo organizado de Releases torna-se praticamente impossível saber:

- quando uma funcionalidade foi entregue;
- quais alterações uma versão possui;
- quais bugs foram corrigidos;
- como retornar para uma versão anterior.

Por esse motivo o Atlas Commerce possui um processo formal de Releases.

---

# O que é uma Release

Uma Release representa uma versão oficial do sistema.

Ela reúne um conjunto de funcionalidades concluídas, documentadas e aprovadas.

Uma Release somente é publicada quando todos os critérios de qualidade forem atendidos.

---

# Evolução do Projeto

```
Pré Projeto

↓

Sprint

↓

Milestone

↓

Release

↓

Nova Sprint
```

Cada Release representa um marco importante na evolução do Atlas Commerce.

---

# Estratégia de Versionamento

O Atlas Commerce utiliza **Semantic Versioning (SemVer)**.

Formato:

```
MAJOR.MINOR.PATCH
```

Exemplo:

```
1.0.0
```

---

# Significado de Cada Número

## MAJOR

Mudanças incompatíveis.

Exemplo:

```
1.x.x

↓

2.0.0
```

Quando ocorre:

- quebra de contrato;
- mudanças incompatíveis na API;
- remoção de funcionalidades.

---

## MINOR

Novas funcionalidades compatíveis.

Exemplo:

```
1.0.0

↓

1.1.0
```

Quando ocorre:

- novos módulos;
- novos endpoints;
- novas funcionalidades.

---

## PATCH

Correções.

Exemplo:

```
1.1.0

↓

1.1.1
```

Quando ocorre:

- correções;
- pequenos ajustes;
- otimizações;
- melhorias internas.

---

# Roadmap das Releases

## Release 0.1.0

Primeira versão técnica.

Entregas:

- Planejamento
- Arquitetura
- Setup
- Documentação inicial

---

## Release 0.2.0

Conclusão do módulo Category.

Entregas:

- CRUD
- Swagger
- Testes
- Documentação
- ADRs

---

## Release 0.3.0

Conclusão do módulo Product.

Entregas:

- Produtos
- Relacionamentos
- Busca
- Paginação

---

## Release 0.4.0

Inventory Module.

---

## Release 0.5.0

Cart Module.

---

## Release 0.6.0

Order Module.

---

## Release 0.7.0

Payment Module.

---

## Release 0.8.0

Authentication.

---

## Release 0.9.0

Observabilidade.

---

## Release 1.0.0

Primeira versão oficial do Atlas Commerce.

---

# Estrutura de uma Release

Cada Release deve conter:

```
Código

+

Documentação

+

ADRs

+

Testes

+

Swagger

+

Migration

+

Release Notes
```

Nenhuma Release é composta apenas por código.

---

# Fluxo de Publicação

```
Feature

↓

Sprint

↓

Code Review

↓

Merge

↓

Build

↓

Testes

↓

Tag

↓

Release

↓

Deploy
```

Todo esse processo deve ser rastreável.

---

# Git Tags

Cada versão publicada deve possuir uma Tag.

Exemplo:

```
v0.1.0

v0.2.0

v0.3.0

v1.0.0
```

Essas Tags permitem recuperar exatamente qualquer versão publicada.

---

# Release Notes

Cada Release deve possuir um documento contendo:

## Novidades

Novas funcionalidades implementadas.

---

## Melhorias

Alterações realizadas.

---

## Correções

Bugs resolvidos.

---

## ADRs

Novas decisões arquiteturais.

---

## Breaking Changes

Caso existam.

---

## Migrações

Novas migrations adicionadas.

---

## Documentação

Arquivos atualizados.

---

# Critérios para Publicação

Uma Release somente poderá ser criada quando:

✔ Todas as Missões estiverem concluídas.

✔ Todos os testes estiverem aprovados.

✔ Swagger atualizado.

✔ ADRs revisadas.

✔ Documentação completa.

✔ Code Review aprovado.

✔ Build funcionando.

---

# Fluxo Visual

```
Missões

↓

Sprint

↓

Milestone

↓

Release Candidate

↓

Release Oficial
```

---

# Release Candidate (RC)

Antes de uma Release oficial poderá existir uma versão candidata.

Exemplo:

```
v1.0.0-RC1

↓

v1.0.0-RC2

↓

v1.0.0
```

Essas versões permitem validações finais.

---

# Histórico de Releases

Toda versão publicada deve permanecer registrada.

Exemplo:

| Versão | Data | Status |
|----------|------------|------------|
| 0.1.0 | Planejamento | Foundation |
| 0.2.0 | Sprint 001 | Category |
| 0.3.0 | Sprint 002 | Product |
| 0.4.0 | Sprint 003 | Inventory |
| 1.0.0 | Primeira versão oficial | Produção |

---

# O que NÃO fazer

Nunca:

- publicar sem testes;
- criar versões sem documentação;
- remover Tags;
- alterar uma Release já publicada;
- ignorar Semantic Versioning.

---

# Boas Práticas

✔ Releases pequenas.

✔ Versionamento semântico.

✔ Release Notes completas.

✔ Tags Git.

✔ Documentação sincronizada.

✔ ADRs atualizadas.

✔ Deploy automatizado.

✔ Histórico preservado.

---

# Benefícios

Esta estratégia proporciona:

- rastreabilidade;
- previsibilidade;
- organização;
- facilidade de rollback;
- histórico confiável;
- evolução controlada.

---

# Relação com Outros Documentos

Este documento complementa:

- ROADMAP.md
- MILESTONE-01.md
- MILESTONE-02.md
- deployment/ci-cd.md
- contribution/git-workflow.md
- commit-convention.md

---

# Decisão Arquitetural

As decisões relacionadas ao processo de Releases seguem:

- ADR-000 — Arquitetura Geral
- ADR-005 — Package by Feature

---

# Referências

- Semantic Versioning (SemVer)
- Git Documentation
- GitHub Releases
- Continuous Delivery
- Spring Boot Documentation

---

# Encerramento da Documentação

Você concluiu toda a documentação estrutural do Atlas Commerce.

A partir deste ponto, os próximos documentos produzidos serão as documentações específicas de cada Missão (MISSION-004 em diante), acompanhando a evolução real do projeto.

Esta documentação passa a servir como um **livro técnico oficial** do Atlas Commerce, reunindo arquitetura, padrões, processos, boas práticas e histórico de evolução do sistema.