# Naming Conventions

## Objetivo

Definir o padrão oficial de nomenclatura utilizado no Atlas Commerce para classes, métodos, variáveis, pacotes, endpoints, tabelas, colunas e demais elementos do projeto.

Uma nomenclatura consistente torna o código previsível, reduz ambiguidades e facilita a manutenção do sistema ao longo do tempo.

---

# Contexto

Uma das maiores causas de dificuldade na leitura de um projeto é a falta de consistência nos nomes utilizados.

Quando cada desenvolvedor adota um estilo diferente, o código perde legibilidade e aumenta a curva de aprendizado para novos membros da equipe.

No Atlas Commerce, todo identificador possui um padrão definido.

---

# Motivação

Um bom nome elimina a necessidade de comentários.

Ao ler:

```java
CategoryRepository
```

fica evidente sua responsabilidade.

Já um nome como:

```java
Repo
```

obriga o leitor a investigar o código.

Nosso objetivo é que cada nome revele claramente sua intenção.

---

# Filosofia

Um bom nome deve ser:

- claro;
- específico;
- curto, mas suficiente;
- consistente;
- previsível.

Sempre prefira clareza à criatividade.

---

# Convenções Gerais

| Elemento | Convenção |
|----------|-----------|
| Classes | PascalCase |
| Interfaces | PascalCase |
| Métodos | camelCase |
| Variáveis | camelCase |
| Constantes | UPPER_SNAKE_CASE |
| Pacotes | lowercase |
| Arquivos | Mesmo nome da classe |
| Endpoints | kebab-case ou plural simples |
| Tabelas | snake_case |
| Colunas | snake_case |

---

# Classes

As classes representam entidades, serviços ou componentes da aplicação.

Utilizam **PascalCase**.

## Correto

```java
Category
```

```java
Product
```

```java
CategoryService
```

```java
CategoryRepository
```

---

## Incorreto

```java
category
```

```java
CATEGORY
```

```java
cat
```

---

# Interfaces

Interfaces seguem o mesmo padrão das classes.

Não utilizamos prefixo "I".

## Correto

```java
CategoryRepository
```

```java
PaymentGateway
```

---

## Incorreto

```java
ICategoryRepository
```

```java
IService
```

---

# Métodos

Métodos representam ações.

Devem iniciar com verbo.

Utilizam **camelCase**.

## Correto

```java
findById()
```

```java
createCategory()
```

```java
deleteProduct()
```

```java
updateInventory()
```

---

## Incorreto

```java
category()
```

```java
process()
```

```java
run()
```

---

# Variáveis

Devem possuir nomes completos.

Evite abreviações.

## Correto

```java
categoryName
```

```java
productPrice
```

```java
customerEmail
```

---

## Incorreto

```java
nm
```

```java
obj
```

```java
tmp
```

---

# Constantes

Constantes utilizam:

UPPER_SNAKE_CASE

## Correto

```java
DEFAULT_PAGE_SIZE
```

```java
MAX_PRODUCTS
```

```java
JWT_EXPIRATION_TIME
```

---

# Pacotes

Todos os pacotes utilizam letras minúsculas.

Nunca utilize CamelCase.

Estrutura:

```
com.atlascommerce
```

↓

```
category
```

↓

```
service
```

Exemplo:

```
com.atlascommerce.category.service
```

---

# Sufixos Oficiais

Cada camada possui um sufixo padronizado.

| Camada | Sufixo |
|---------|---------|
| Controller | Controller |
| Service | Service |
| Repository | Repository |
| Mapper | Mapper |
| Validator | Validator |
| Specification | Specification |
| Entity | sem sufixo |
| DTO | Request / Response |

---

# DTOs

Request:

```java
CreateCategoryRequest
```

```java
UpdateCategoryRequest
```

Response:

```java
CategoryResponse
```

Nunca utilizar:

```java
CategoryDTO
```

O nome deve indicar claramente sua finalidade.

---

# Entidades

As entidades representam conceitos do domínio.

Sempre no singular.

## Correto

```java
Category
```

```java
Product
```

```java
Order
```

---

## Incorreto

```java
Categories
```

```java
Products
```

---

# Repositórios

Sempre terminam com:

```
Repository
```

Exemplo:

```java
CategoryRepository
```

---

# Serviços

Sempre terminam com:

```
Service
```

Exemplo:

```java
CategoryService
```

---

# Controllers

Sempre terminam com:

```
Controller
```

Exemplo:

```java
CategoryController
```

---

# Exceptions

Todas terminam com:

```
Exception
```

Exemplo:

```java
CategoryNotFoundException
```

```java
DuplicateCategoryException
```

---

# Enumerações

Utilizam PascalCase.

Valores internos utilizam UPPER_CASE.

```java
public enum OrderStatus {

    CREATED,

    PAID,

    SHIPPED,

    DELIVERED

}
```

---

# Endpoints REST

Sempre:

- substantivos;
- plural;
- minúsculo.

## Correto

```
/categories
```

```
/products
```

```
/orders
```

---

## Incorreto

```
/getCategories
```

```
/CreateProduct
```

```
/DeleteOrder
```

O verbo pertence ao método HTTP.

---

# Tabelas

Utilizam snake_case.

Plural.

Exemplo:

```
categories
```

```
products
```

```
orders
```

---

# Colunas

Sempre em snake_case.

Exemplo:

```
created_at
```

```
updated_at
```

```
category_name
```

---

# Campos UUID

Sempre utilizar:

```
id
```

Para relacionamentos:

```
category_id
```

```
product_id
```

---

# Variáveis Booleanas

Devem responder perguntas.

Exemplo:

```java
isActive
```

```java
hasPermission
```

```java
canDelete
```

Evite:

```java
flag
```

```java
status
```

---

# Métodos Booleanos

Devem iniciar por:

- is
- has
- can
- should

Exemplo:

```java
isAvailable()
```

```java
hasStock()
```

```java
canDelete()
```

---

# Diagramas

## Estrutura de Nomeação

```
Category

↓

CategoryController

↓

CategoryService

↓

CategoryRepository

↓

CategoryResponse
```

Toda feature segue exatamente a mesma convenção.

---

# Fluxo de Desenvolvimento

```
Criar Feature

↓

Definir Nome

↓

Criar Classe

↓

Criar Serviço

↓

Criar Repository

↓

Criar DTO

↓

Criar Controller
```

A consistência na nomenclatura facilita a navegação pelo projeto.

---

# Boas Práticas

- Utilize nomes completos.
- Evite abreviações.
- Seja consistente em todo o projeto.
- Nomeie conforme a responsabilidade.
- Utilize verbos para métodos.
- Utilize substantivos para classes.
- Mantenha o mesmo padrão em todos os módulos.

---

# Erros Comuns

- Misturar português e inglês.
- Usar abreviações sem significado.
- Criar nomes genéricos como `Manager`, `Helper` ou `Utils`.
- Utilizar siglas desconhecidas.
- Criar nomes excessivamente longos.

---

# Relação com Outros Documentos

- standards/coding-standards.md
- standards/clean-code.md
- standards/package-structure.md
- architecture/package-architecture.md
- contribution/code-review.md

---

# Referências

- Clean Code — Robert C. Martin
- Effective Java — Joshua Bloch
- Java Code Conventions (Oracle)
- Spring Boot Reference Documentation

---

# Próximo Capítulo

package-structure.md