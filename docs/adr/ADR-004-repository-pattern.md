
---

# `docs/adr/ADR-004-repository-pattern.md`

```markdown
# ADR-004 — Repository Pattern

## Status

Accepted

---

## Objetivo

Definir o padrão de acesso aos dados utilizado pelo Atlas Commerce.

---

## Contexto

A aplicação precisa separar as regras de negócio da infraestrutura responsável pela persistência.

Os domínios do sistema realizarão operações como:

- criação
- consulta
- atualização
- remoção
- filtros
- buscas específicas

Essas operações não devem ficar dentro dos Controllers ou misturadas com regras de negócio.

---

## Problema

Acesso direto ao banco dentro de Controllers ou Services pode aumentar o acoplamento entre negócio e infraestrutura.

Exemplo inadequado:

```text
Controller
   ↓
Database