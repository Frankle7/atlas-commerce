
---

# `docs/adr/ADR-005-package-by-feature.md`

```markdown
# ADR-005 — Package by Feature

## Status

Accepted

---

## Objetivo

Definir a estratégia oficial de organização dos pacotes do Atlas Commerce.

---

## Contexto

O Atlas Commerce possui múltiplos domínios de negócio.

Entre eles:

- Category
- Product
- Order
- Payment
- User
- Cart
- Inventory
- Authentication

À medida que o sistema cresce, uma estrutura baseada exclusivamente em camadas pode espalhar arquivos de uma mesma Feature por diferentes partes do projeto.

Exemplo:

```text
controller/
service/
repository/
entity/