
---

# `docs/adr/ADR-003-uuid.md`

Esse é o seu ADR que já existia. **Aqui apenas corrigimos a numeração e padronizamos.**

```markdown
# ADR-003 — UUID como Estratégia de Identificação

## Status

Accepted

---

## Objetivo

Definir a estratégia oficial de identificação das entidades do Atlas Commerce.

---

## Contexto

O Atlas Commerce é um projeto desenvolvido para simular um e-commerce moderno, com foco em arquitetura escalável e boas práticas de engenharia de software.

Precisamos definir qual estratégia será utilizada para identificar as entidades do sistema.

As principais opções avaliadas foram:

- BIGINT
- UUID

---

## Problema

Identificadores sequenciais podem tornar os recursos da API previsíveis.

Exemplo:

```text
/products/1
/products/2
/products/3