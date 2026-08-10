# Paginação

---

# Objetivo

Definir a estratégia oficial de paginação utilizada pelo Atlas Commerce para consultas REST.

Ao final deste capítulo o desenvolvedor será capaz de compreender:

- como realizar consultas paginadas
- como ordenar resultados
- como utilizar filtros
- como funciona o objeto Page do Spring Data
- padrões adotados pelo Atlas Commerce
- boas práticas para consultas performáticas

Este documento estabelece um contrato único para todas as consultas que retornam coleções de dados.

---

# Contexto

Sistemas de e-commerce armazenam milhares ou milhões de registros.

Exemplos:

- Produtos
- Categorias
- Pedidos
- Clientes
- Estoque
- Pagamentos

Retornar todos esses registros em uma única resposta torna a API lenta, aumenta o consumo de memória e gera uma experiência ruim para o cliente.

Por esse motivo toda consulta que retorna listas deverá utilizar paginação.

---

# Motivação

Imagine uma loja contendo:

```
2.300.000 produtos
```

Uma requisição como:

```
GET /products
```

retornando todos os registros exigiria:

- alto consumo de memória
- aumento do tempo de resposta
- sobrecarga do banco de dados
- tráfego excessivo de rede

A paginação resolve esse problema dividindo os dados em pequenas páginas.

---

# Funcionamento Geral

```
Cliente

↓

GET /products?page=0&size=20

↓

Controller

↓

Service

↓

Repository

↓

PostgreSQL

↓

Page<Product>

↓

JSON
```

---

# Parâmetros Oficiais

O Atlas Commerce adota os parâmetros padrão do Spring Data.

| Parâmetro | Descrição |
|-----------|-----------|
| page | Número da página |
| size | Quantidade de registros |
| sort | Ordenação |

Exemplo

```
GET /products?page=0&size=20
```

---

# Número da Página

A primeira página sempre será:

```
page=0
```

Exemplo

```
GET /categories?page=0
```

Segunda página

```
page=1
```

Terceira página

```
page=2
```

---

# Quantidade de Registros

O parâmetro size define quantos registros serão retornados.

Exemplo

```
GET /products?page=0&size=20
```

Retorna:

```
20 produtos
```

---

# Limite Máximo

Para evitar consultas excessivas, o Atlas Commerce define um limite máximo de registros por página.

```
Máximo permitido

100 registros
```

Caso o cliente solicite:

```
size=500
```

A API poderá:

- limitar automaticamente para 100
- ou retornar erro de validação

Essa decisão será definida pela camada de configuração da aplicação.

---

# Ordenação

A ordenação utiliza o parâmetro:

```
sort
```

Formato

```
sort=campo,direção
```

Exemplo

```
GET /products?sort=name,asc
```

ou

```
GET /products?sort=price,desc
```

Também é possível combinar múltiplas ordenações.

```
sort=category,asc&sort=name,asc
```

---

# Resposta da API

Exemplo

```json
{
    "content":[
        {
            "id":"1",
            "name":"Notebook"
        },
        {
            "id":"2",
            "name":"Mouse"
        }
    ],
    "page":0,
    "size":20,
    "totalElements":250,
    "totalPages":13,
    "first":true,
    "last":false
}
```

---

# Estrutura da Resposta

| Campo | Descrição |
|--------|-----------|
| content | Lista de registros |
| page | Página atual |
| size | Quantidade por página |
| totalElements | Total de registros |
| totalPages | Total de páginas |
| first | Primeira página |
| last | Última página |

---

# Fluxo da Paginação

```
Cliente

↓

?page=0

↓

Controller

↓

Service

↓

Repository

↓

Pageable

↓

Database

↓

Page<T>

↓

JSON
```

---

# Classe Pageable

O Atlas Commerce utilizará a interface padrão do Spring Data.

Exemplo

```java
Page<Category> findAll(Pageable pageable);
```

A responsabilidade da paginação pertence ao banco de dados, evitando carregamento desnecessário em memória.

---

# Filtros

A paginação pode ser combinada com filtros.

Exemplo

```
GET /products

?page=0

&size=20

&category=electronics

&active=true
```

Outro exemplo

```
GET /orders

?page=0

&status=PAID
```

---

# Pesquisa

Também será possível combinar paginação com pesquisa textual.

Exemplo

```
GET /products

?search=iphone

&page=0

&size=20
```

---

# Ordenação + Pesquisa

Exemplo

```
GET /products

?search=iphone

&page=0

&size=20

&sort=price,asc
```

---

# Boas Práticas

✔ Sempre utilizar paginação para listas.

✔ Nunca retornar milhares de registros.

✔ Definir tamanho máximo da página.

✔ Permitir ordenação.

✔ Utilizar índices no banco de dados.

✔ Ordenar por campos indexados sempre que possível.

✔ Documentar todos os parâmetros disponíveis.

---

# Performance

A paginação reduz:

- consumo de memória
- tempo de resposta
- tráfego de rede
- carga no banco de dados

Ela é um dos principais mecanismos para escalabilidade de APIs REST.

---

# Erros Comuns

❌ Permitir `size` ilimitado.

❌ Ordenar por campos não indexados.

❌ Retornar listas completas.

❌ Ignorar parâmetros inválidos.

❌ Misturar paginação manual com Spring Data.

---

# Decisão Arquitetural

Esta estratégia está relacionada às ADRs:

- ADR-000 — Arquitetura do Projeto
- ADR-004 — Repository Pattern
- ADR-006 — Category Domain

---

# Referências

- Spring Data JPA
- Spring Pageable
- RFC 9110
- REST API Design Guidelines
- Microsoft REST API Guidelines

---

# Próximo Capítulo

architecture/architecture.md

Nos próximos capítulos a documentação deixa de abordar apenas a API e passa a explorar a arquitetura completa do Atlas Commerce, incluindo organização dos módulos, fluxo das requisições, divisão em camadas, princípios arquiteturais e decisões de projeto que sustentam toda a aplicação.