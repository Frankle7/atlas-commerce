# Pull Request Template

---

# Objetivo

Definir o modelo oficial utilizado para criação de Pull Requests no Atlas Commerce.

Este documento estabelece quais informações devem estar presentes em uma solicitação de alteração, garantindo que toda mudança possua contexto, justificativa, evidências e validação adequada.

---

# Contexto

Pull Requests são o ponto de integração entre desenvolvimento e revisão.

Eles representam uma etapa importante do ciclo de vida do código:

```
Desenvolvimento

↓

Feature Branch

↓

Pull Request

↓

Code Review

↓

Merge
```

Um Pull Request bem estruturado facilita a análise, reduz erros e mantém o histórico do projeto organizado.

---

# Motivação

Um padrão único de Pull Request permite:

- facilitar revisões;
- melhorar comunicação;
- registrar decisões técnicas;
- identificar impactos;
- manter rastreabilidade.

Toda alteração no Atlas Commerce deve possuir um Pull Request seguindo este modelo.

---

# Modelo Oficial

Todo Pull Request deve utilizar a seguinte estrutura.

---

# Título do Pull Request

O título deve seguir o padrão:

```
tipo(modulo): descrição da alteração
```

Exemplos:

```
feat(category): create category service

fix(authentication): fix jwt validation

docs(api): update error documentation

test(product): add product repository tests
```

O título deve ser objetivo e representar a principal mudança.

---

# Descrição

## Resumo

Explique brevemente o que foi desenvolvido.

Exemplo:

```
Implementação inicial do domínio Category,
incluindo entidade, repository e migration PostgreSQL.
```

---

# Motivação

Explique por que essa alteração foi necessária.

Exemplo:

```
A Missão 004 inicia a implementação do domínio Category,
responsável pelo gerenciamento das categorias de produtos.
```

---

# Missão Relacionada

Toda alteração deve informar qual missão pertence.

Exemplo:

```
Relacionado:

MISSION-004 — Category Domain
```

---

# Tipo de Alteração

Marque o tipo principal:

```
[x] Feature

[ ] Bug Fix

[ ] Refactor

[ ] Documentation

[ ] Test

[ ] Chore
```

---

# Alterações Realizadas

Liste todas as mudanças.

Exemplo:

```
- Criada entidade Category
- Criado CategoryRepository
- Criada migration V001
- Adicionado ADR-006
- Atualizada documentação do domínio
```

---

# Arquivos Principais Alterados

Informe os arquivos mais importantes.

Exemplo:

```
backend/atlas-api/

src/main/java/com/atlascommerce/category/entity/Category.java

src/main/java/com/atlascommerce/category/repository/CategoryRepository.java

src/main/resources/db/migration/V001__create_category_table.sql
```

---

# Impacto da Alteração

Descreva quais áreas foram afetadas.

Exemplo:

```
Impacto:

Novo domínio disponível para futuras integrações.

Nenhuma API existente foi alterada.
```

---

# Decisões Técnicas

Registrar decisões importantes.

Exemplo:

```
Foi adotado Package by Feature conforme ADR-005.

O acesso ao banco permanece isolado através do Repository Pattern.
```

---

# Evidências

Adicionar informações que comprovem funcionamento.

Exemplo:

```
Testes executados:

mvn test

Resultado:

BUILD SUCCESS
```

---

# Testes Realizados

Informar testes executados.

Exemplo:

```
[x] Teste unitário

[x] Teste integração

[x] Teste manual

[ ] Não aplicável
```

---

# Checklist Obrigatório

Antes da aprovação, confirmar:

```
## Código

[x] Código segue padrões do projeto

[x] Responsabilidades estão separadas

[x] Não existem arquivos temporários


## Arquitetura

[x] Segue Package by Feature

[x] Respeita ADRs existentes

[x] Não cria dependências desnecessárias


## Documentação

[x] Documentação atualizada

[x] ADR criado quando necessário

[x] README atualizado quando necessário


## Testes

[x] Testes executados

[x] Código compilando

[x] Sem erros conhecidos
```

---

# Reviewers

Adicionar responsáveis pela revisão.

Exemplo:

```
Reviewers:

- Backend Team
- Architecture Owner
```

---

# Dependências

Informar se existe dependência externa.

Exemplo:

```
Dependências:

Nenhuma.

```

Ou:

```
Depende da conclusão:

MISSION-003 — Setup Project
```

---

# Screenshots / Evidências Visuais

Quando existir alteração visual:

Adicionar:

- imagens;
- vídeos;
- exemplos de resposta API;
- documentação Swagger.

---

# Breaking Changes

Informar se existe alteração incompatível.

Exemplo:

```
Breaking Change:

Não.

```

Caso exista:

```
Breaking Change:

Endpoint /api/v1/categories alterado.

Necessária criação da versão /api/v2.
```

---

# Exemplo Completo

## Pull Request

```
feat(category): create category domain
```

---

## Resumo

Implementação inicial do domínio Category.

---

## Missão

```
MISSION-004
```

---

## Alterações

```
- Category Entity
- Category Repository
- Database Migration
- ADR Category Domain
- Documentation
```

---

## Testes

```
mvn test

BUILD SUCCESS
```

---

## Resultado Esperado

O sistema passa a possuir a base necessária para evolução do catálogo de produtos.

---

# Regras de Aprovação

Um Pull Request somente pode ser aprovado quando:

- código estiver revisado;
- testes passarem;
- documentação estiver atualizada;
- padrões arquiteturais forem respeitados.

---

# O que NÃO fazer

Nunca:

- abrir PR sem descrição;
- misturar várias missões;
- ignorar documentação;
- fazer merge sem revisão;
- aprovar código sem testes.

---

# Boas Práticas

✔ Pull Requests pequenos.

✔ Descrições claras.

✔ Uma missão por PR.

✔ Commits organizados.

✔ Evidências anexadas.

✔ Revisão técnica antes do merge.

---

# Fluxo Final


```
Feature

↓

Commit

↓

Push

↓

Pull Request

↓

Code Review

↓

Sprint

↓

Release

↓

Main
```

---

# Relação com Outros Documentos

Este documento complementa:

- contribution.md
- code-review.md
- commit-convention.md
- git-workflow.md

---

# Referências

- GitHub Pull Requests
- Conventional Commits
- Code Review Practices
- Software Engineering Best Practices

---

# Próximo Capítulo

deployment/deployment.md