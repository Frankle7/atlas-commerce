# Módulo 04 — Arquitetura dos Módulos

# module-diagram.md

---

# Objetivo

Apresentar todos os módulos do Atlas Commerce e demonstrar como eles se relacionam dentro da arquitetura da aplicação.

Este documento serve como o mapa geral do sistema e permite compreender rapidamente onde cada responsabilidade está localizada.

---

# Contexto

O Atlas Commerce foi projetado utilizando a arquitetura **Package by Feature**.

Cada domínio de negócio é organizado como um módulo independente, contendo todas as camadas necessárias para sua implementação.

Essa abordagem facilita:

- manutenção;
- escalabilidade;
- testes;
- baixo acoplamento;
- alta coesão.

---

# Organização Geral

```

Atlas Commerce

├── Auth
├── User
├── Category
├── Product
├── Inventory
├── Cart
├── Order
├── Payment
├── Address
├── Notification
└── Shared

```

Cada módulo representa um domínio específico da aplicação.

---

# Diagrama Geral

```

                    +-------------+
                    | Authentication |
                    +------+------+
                           |
                           |
            +--------------+--------------+
            |                             |
      +-----v-----+                 +-----v-----+
      |   User    |                 |  Address  |
      +-----------+                 +-----------+

                           |
                           |

+-----------+      +-------------+      +-------------+
| Category  | ---> |  Product    | ---> | Inventory   |
+-----------+      +-------------+      +-------------+

                           |
                           |

                    +------+------+
                    |    Cart     |
                    +------+------+
                           |
                           |

                    +------+------+
                    |    Order    |
                    +------+------+
                           |
                 +---------+----------+
                 |                    |
         +-------v------+     +-------v-------+
         |   Payment    |     | Notification  |
         +--------------+     +---------------+

```

---

# Dependências entre módulos

```

Category
↓

Product
↓

Inventory
↓

Cart
↓

Order
↓

Payment

```

A direção da seta representa dependência lógica.

Exemplo:

Product depende de Category.

Category não conhece Product.

---

# Descrição dos módulos

## Authentication

Responsável pela autenticação da aplicação.

Responsabilidades

- Login
- Refresh Token
- JWT
- Segurança

Expõe

- Login API
- Token API

---

## User

Gerencia usuários do sistema.

Responsabilidades

- Cadastro
- Perfil
- Atualização
- Permissões

---

## Category

Representa categorias de produtos.

Responsabilidades

- CRUD
- Hierarquia
- Ativação
- Ordenação

É utilizado por:

- Product

---

## Product

Responsável pelo catálogo.

Responsabilidades

- Produtos
- Preços
- Imagens
- SKU
- Categoria

Depende de:

- Category

---

## Inventory

Gerencia estoque.

Responsabilidades

- Quantidade
- Reserva
- Entrada
- Saída

Depende de:

- Product

---

## Cart

Carrinho do usuário.

Responsabilidades

- Adicionar itens
- Remover itens
- Atualizar quantidade
- Calcular subtotal

Depende de:

- Product
- Inventory

---

## Order

Pedido.

Responsabilidades

- Criar pedido
- Histórico
- Status
- Cancelamento

Depende de:

- Cart
- User
- Address

---

## Payment

Processamento financeiro.

Responsabilidades

- PIX
- Cartão
- Boleto
- Gateway

Depende de:

- Order

---

## Notification

Envio de mensagens.

Responsabilidades

- Email
- SMS
- Push

Depende de:

- Order
- Payment

---

## Shared

Contém componentes reutilizáveis.

Exemplos

- Exceptions
- Validators
- Utils
- Configurações
- DTOs comuns

Todos os módulos podem utilizar o Shared.

---

# Fluxo simplificado

```

Usuário

↓

Authentication

↓

Category

↓

Product

↓

Cart

↓

Order

↓

Payment

↓

Notification

```

---

# Princípios adotados

Cada módulo deve possuir:

- Controller
- Service
- Repository
- Entity
- DTO
- Mapper
- Validator
- Specification

Nenhum módulo acessa diretamente outro banco de dados.

Toda comunicação acontece através da camada Service.

---

# Regras Arquiteturais

✅ Um módulo não pode acessar Repository de outro módulo.

✅ Controllers nunca conversam entre si.

✅ Services representam a regra de negócio.

✅ Repository apenas persiste dados.

✅ DTO nunca acessa banco.

✅ Mapper não contém regra de negócio.

---

# Benefícios

Esta arquitetura proporciona:

- baixo acoplamento;
- fácil manutenção;
- alta escalabilidade;
- testes independentes;
- organização por domínio.

---

# Relação com outros documentos

Este capítulo complementa:

- architecture.md
- package-architecture.md
- request-flow.md

Para detalhes internos de cada módulo consulte:

- package-architecture.md

---

# Referências

- Domain Driven Design — Eric Evans
- Clean Architecture — Robert C. Martin
- Spring Modulith
- Package by Feature

---

# Próximo Capítulo

database-architecture.md

```

---

Esse capítulo conclui a visão da **arquitetura de software**. O próximo (`database-architecture.md`) entra na arquitetura de dados: modelagem, relacionamentos, convenções de tabelas, migrations (Flyway), índices, chaves estrangeiras e boas práticas de banco de dados.