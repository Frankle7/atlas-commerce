## O que existe dentro de um e-commerce?
Usuários
Produtos
Categorias
Pedidos
Pagamentos
Carrinho
Avaliações
Favoritos

## Identificar as entidades
User
Role
Address

Product
Category
Brand
ProductImage
Inventory   

Cart
CartItem

Order
OrderItem

Payment

Coupon

Review

Favorite

Notification

AuditLog

## Descobrir os relacionamentos
User
 ├── possui vários Address
 ├── possui vários Orders
 ├── possui vários Favorites
 ├── possui vários Reviews

Product
 ├── pertence a uma Category
 ├── possui várias Images
 ├── possui um Inventory
 ├── possui várias Reviews

Order
 ├── pertence a um User
 ├── possui vários OrderItems
 ├── possui um Payment

 ## o primeiro diagrama
 User
 │
 ├──── Address
 │
 ├──── Order
 │        │
 │        ├──── Payment
 │        └──── OrderItem
 │
 ├──── Favorite
 │
 └──── Review

Product
 │
 ├──── Category
 ├──── ProductImage
 ├──── Inventory
 └──── Review