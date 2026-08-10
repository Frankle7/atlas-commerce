# Coding Standards

## Objetivo

Definir o padrão oficial de desenvolvimento utilizado no Atlas Commerce.

Este documento estabelece regras de escrita de código, organização, nomenclatura, estrutura, boas práticas e princípios arquiteturais para garantir que todo o projeto mantenha consistência, legibilidade e facilidade de manutenção.

O objetivo não é apenas definir regras, mas explicar **o motivo** de cada decisão.

---

# Contexto

Um projeto de software cresce continuamente.

Novos desenvolvedores entram.

Novas funcionalidades são implementadas.

Refatorações acontecem.

Sem um padrão claro, o código rapidamente se torna inconsistente.

O Atlas Commerce adota um conjunto de convenções inspirado em projetos utilizados por empresas como Stripe, Netflix, Uber e Google.

---

# Motivação

Escrever código é simples.

Escrever código que continuará sendo compreendido daqui a cinco anos é difícil.

Os padrões definidos neste documento possuem cinco objetivos principais:

- aumentar a legibilidade;
- facilitar manutenção;
- reduzir bugs;
- simplificar revisões de código;
- manter consistência arquitetural.

---

# Filosofia do Projeto

No Atlas Commerce seguimos alguns princípios fundamentais.

```
Código limpo

>

Código inteligente
```

```
Legibilidade

>

Complexidade
```

```
Simplicidade

>

Otimização prematura
```

```
Consistência

>

Criatividade
```

Sempre que houver dúvida entre duas implementações, escolha a mais simples.

---

# Princípios Gerais

Todo código deve obedecer aos seguintes princípios:

- legível;
- previsível;
- reutilizável;
- desacoplado;
- testável;
- documentado.

---

# Clean Code

Seguimos os princípios apresentados por Robert C. Martin.

Boas práticas:

- funções pequenas;
- classes coesas;
- responsabilidades únicas;
- nomes autoexplicativos;
- baixa complexidade;
- evitar duplicação.

Exemplo:

❌

```java
public void p(){}
```

✔

```java
public void createCategory(Category category){}
```

O nome da função deve explicar exatamente sua responsabilidade.

---

# SOLID

Todo desenvolvimento deve respeitar os princípios SOLID.

## Single Responsibility

Cada classe possui apenas uma responsabilidade.

```
CategoryService

↓

Regras de negócio
```

Não deve validar requisições HTTP.

Não deve acessar diretamente o banco.

---

## Open / Closed

Classes devem estar abertas para extensão.

Fechadas para modificação.

---

## Liskov

Implementações devem respeitar contratos.

---

## Interface Segregation

Interfaces pequenas.

Evite interfaces gigantes.

---

## Dependency Inversion

Dependa de abstrações.

Nunca de implementações concretas.

---

# Organização dos Arquivos

Cada Feature possui exatamente a mesma estrutura.

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

Isso reduz a curva de aprendizado.

---

# Tamanho das Classes

Recomendação:

| Elemento | Máximo recomendado |
|----------|--------------------|
| Classe | 300 linhas |
| Método | 30 linhas |
| Controller | 200 linhas |
| Service | 300 linhas |

Não é uma regra absoluta.

É um indicativo de necessidade de refatoração.

---

# Nomeação

Utilize nomes claros.

Evite abreviações.

✔

```java
CategoryRepository
```

❌

```java
CatRepo
```

---

# Métodos

Métodos devem representar ações.

Utilize verbos.

✔

```
findById()

create()

update()

delete()
```

Evite:

```
execute()

process()

handle()
```

quando não expressarem claramente a responsabilidade.

---

# Variáveis

Prefira nomes completos.

✔

```java
categoryName
```

❌

```java
cn
```

---

# Constantes

Sempre em maiúsculas.

```java
MAX_PAGE_SIZE

DEFAULT_PAGE_SIZE
```

---

# DTOs

DTOs representam comunicação.

Nunca regras de negócio.

Nunca acesso ao banco.

---

# Controllers

Responsabilidades:

- receber requisições;
- validar entrada;
- retornar respostas.

Nunca implementar regras de negócio.

Fluxo:

```
Request

↓

Controller

↓

Service

↓

Repository
```

---

# Services

Concentram toda regra de negócio.

Podem chamar:

- Repository;
- Validators;
- Mappers;
- Outros Services.

Nunca acessar HTTP.

---

# Repository

Responsável exclusivamente pela persistência.

Nunca implementar regras de negócio.

---

# Entities

Representam tabelas do banco.

Não devem conter lógica de aplicação.

---

# Exceptions

Nunca utilizar:

```java
throw new Exception();
```

Sempre criar exceções específicas.

Exemplo:

```java
CategoryNotFoundException
```

---

# Logging

Registrar apenas informações relevantes.

Evite:

- logs duplicados;
- stack traces desnecessárias;
- informações sensíveis.

---

# Comentários

Código deve ser autoexplicativo.

Comentários existem apenas quando agregam contexto.

Evite:

```java
// soma dois números
```

Prefira documentação arquitetural quando necessário.

---

# Formatação

Indentação:

```
4 espaços
```

Comprimento máximo recomendado:

```
120 caracteres
```

Sempre utilizar UTF-8.

---

# Imports

Organizar automaticamente pela IDE.

Nunca utilizar wildcard.

❌

```java
import java.util.*;
```

✔

```java
import java.util.List;
```

---

# Tratamento de Erros

Toda exceção deve possuir:

- mensagem clara;
- contexto;
- tratamento centralizado.

Utilizamos Global Exception Handler.

---

# Testabilidade

Todo código deve ser escrito pensando em testes.

Evite dependências difíceis de simular.

Prefira injeção de dependências.

---

# Performance

Antes de otimizar:

- medir;
- identificar gargalos;
- justificar mudanças.

Nunca otimizar sem necessidade.

---

# Segurança

Nunca:

- expor senhas;
- armazenar tokens em texto puro;
- registrar dados sensíveis em logs.

Sempre validar entradas.

---

# Documentação

Toda alteração significativa deve atualizar:

- Mission correspondente;
- ADR (quando necessário);
- documentação da API;
- documentação arquitetural.

Código e documentação evoluem juntos.

---

# Fluxo de Desenvolvimento

```
Planejamento

↓

Implementação

↓

Testes

↓

Documentação

↓

Review

↓

Merge
```

---

# Checklist Antes do Commit

Antes de realizar um commit, confirme:

- Código compila.
- Testes executam.
- Convenções respeitadas.
- Imports organizados.
- Código formatado.
- Documentação atualizada.
- Sem código comentado.
- Sem TODOs desnecessários.

---

# Boas Práticas

- Escreva código simples.
- Faça uma única coisa por método.
- Evite duplicação.
- Prefira composição à herança.
- Utilize nomes claros.
- Mantenha classes pequenas.
- Atualize a documentação sempre que necessário.

---

# Erros Comuns

- Classes gigantes.
- Métodos muito longos.
- Controllers com regras de negócio.
- Duplicação de código.
- Comentários desnecessários.
- Exceções genéricas.
- Dependências acopladas.
- Código sem testes.

---

# Relação com Outros Documentos

- standards/clean-code.md
- standards/naming.md
- standards/package-structure.md
- standards/commit-convention.md
- contribution/code-review.md
- architecture/package-architecture.md

---

# Referências

- Clean Code — Robert C. Martin
- Clean Architecture — Robert C. Martin
- Effective Java — Joshua Bloch
- Refactoring — Martin Fowler
- Spring Boot Reference Documentation
- Google Java Style Guide

---

# Próximo Capítulo

clean-code.md