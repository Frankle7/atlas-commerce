# Atlas Commerce - Domain Model

Este documento descreve as principais entidades do domínio do Atlas Commerce e suas responsabilidades dentro da plataforma.

---

# User

Representa qualquer pessoa autenticada na plataforma.

## Responsabilidades

- Realizar autenticação.
- Gerenciar seu perfil.
- Gerenciar seus endereços.
- Adicionar produtos aos favoritos.
- Adicionar produtos ao carrinho.
- Realizar compras.
- Acompanhar pedidos.
- Avaliar produtos.

## Relacionamentos

- 1:N Address
- 1:N Order
- 1:N Review
- 1:N Favorite
- 1:1 Cart

---

# Role

Define o nível de acesso de um usuário dentro da plataforma.

## Exemplos

- ADMIN
- MANAGER
- CUSTOMER

## Relacionamentos

- 1:N User

---

# Address

Representa um endereço de entrega pertencente a um usuário.

## Responsabilidades

- Armazenar endereço de entrega.
- Definir endereço principal.

## Relacionamentos

- N:1 User

---

# Product

Representa um produto disponível para venda.

## Responsabilidades

- Exibir informações do produto.
- Controlar preço.
- Controlar disponibilidade.

## Relacionamentos

- N:1 Category
- N:1 Brand
- 1:N ProductImage
- 1:1 Inventory
- 1:N Review

---

# Category

Agrupa produtos semelhantes.

## Relacionamentos

- 1:N Product

---

# Brand

Representa a marca fabricante do produto.

## Relacionamentos

- 1:N Product

---

# ProductImage

Representa uma imagem de um produto.

## Relacionamentos

- N:1 Product

---

# Inventory

Controla o estoque de um produto.

## Responsabilidades

- Quantidade disponível.
- Reserva de estoque.
- Atualização após venda.

## Relacionamentos

- 1:1 Product

---

# Cart

Representa o carrinho de compras de um usuário.

## Relacionamentos

- 1:1 User
- 1:N CartItem

---

# CartItem

Representa um produto dentro do carrinho.

## Relacionamentos

- N:1 Cart
- N:1 Product

---

# Order

Representa uma compra realizada.

## Responsabilidades

- Armazenar status.
- Valor total.
- Data da compra.

## Relacionamentos

- N:1 User
- 1:N OrderItem
- 1:1 Payment

---

# OrderItem

Representa um produto comprado em um pedido.

## Relacionamentos

- N:1 Order
- N:1 Product

---

# Payment

Representa o pagamento de um pedido.

## Responsabilidades

- Método de pagamento.
- Status.
- Valor.

## Relacionamentos

- 1:1 Order

---

# Coupon

Representa um cupom de desconto.

## Responsabilidades

- Aplicar desconto.
- Definir validade.
- Controlar limite de uso.

---

# Review

Representa a avaliação feita por um cliente.

## Relacionamentos

- N:1 User
- N:1 Product

---

# Favorite

Representa um produto favoritado por um usuário.

## Relacionamentos

- N:1 User
- N:1 Product

---

# Notification

Representa notificações enviadas ao usuário.

## Responsabilidades

- Informar mudanças no pedido.
- Informar promoções.
- Informar atualizações da conta.

## Relacionamentos

- N:1 User

---

# AuditLog

Registra ações importantes realizadas na plataforma.

## Responsabilidades

- Registrar login.
- Registrar alterações de dados.
- Registrar operações administrativas.

## Relacionamentos

- N:1 User