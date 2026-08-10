# PostgreSQL

---

# Objetivo

Definir o padrão oficial de utilização do PostgreSQL no Atlas Commerce.

Este documento explica por que o PostgreSQL foi escolhido, como sua estrutura foi organizada, quais convenções devem ser seguidas e como o banco evolui ao longo do projeto.

Ao concluir este capítulo, o desenvolvedor compreenderá a arquitetura do banco de dados, o fluxo de criação das tabelas e as boas práticas adotadas pela equipe.

---

# Contexto

O banco de dados é um dos pilares do Atlas Commerce.

Toda informação crítica da plataforma é armazenada de forma relacional, garantindo consistência, integridade e segurança.

Entre os principais dados persistidos estão:

- usuários;
- produtos;
- categorias;
- pedidos;
- pagamentos;
- estoque;
- autenticação.

Toda a modelagem foi projetada pensando em escalabilidade e facilidade de manutenção.

---

# Motivação

A escolha do PostgreSQL foi baseada em sua maturidade e confiabilidade.

Principais vantagens:

- software open source;
- alta performance;
- suporte completo a SQL;
- excelente suporte ao Spring Boot;
- compatibilidade com Docker;
- recursos avançados de indexação;
- suporte nativo a UUID;
- alta confiabilidade para aplicações de grande porte.

Essas características tornam o PostgreSQL uma excelente escolha para aplicações de e-commerce.

---

# Arquitetura Geral

```
Cliente

↓

Spring Boot

↓

Spring Data JPA

↓

Hibernate

↓

PostgreSQL

↓

Disco
```

Toda comunicação com o banco acontece através do Spring Data JPA.

Nenhuma consulta SQL deve ser realizada diretamente pelos Controllers.

---

# Organização do Banco

O banco segue uma modelagem baseada em domínios.

Cada módulo possui suas próprias tabelas.

```
Database

├── category

├── product

├── order

├── customer

├── payment

├── inventory

├── notification

└── user
```

Essa divisão facilita a evolução da aplicação.

---

# Estrutura de Diretórios

```
database/

├── docs/

├── migrations/

├── schema/

└── seed/
```

Cada pasta possui uma responsabilidade específica.

---

## docs/

Contém toda a documentação da modelagem.

Exemplos:

- domínio;
- regras de negócio;
- relacionamentos;
- modelo ER.

---

## migrations/

Armazena todas as versões do banco.

Exemplo:

```
V001__create_category_table.sql

V002__create_product_table.sql

V003__create_order_table.sql
```

Cada alteração estrutural gera uma nova migration.

---

## schema/

Armazena diagramas da base de dados.

Exemplo:

```
atlas-commerce-er-diagram.drawio
```

---

## seed/

Contém scripts opcionais para popular o banco durante desenvolvimento.

Exemplo:

```
categories.sql

products.sql

users.sql
```

---

# Convenção das Tabelas

Todas as tabelas seguem padrão único.

Exemplo:

```
category

product

customer

order_item

payment
```

Utilizamos:

- letras minúsculas;
- snake_case;
- nomes no singular quando representam entidade.

---

# Convenção das Colunas

Exemplo.

```
id

name

description

created_at

updated_at

deleted_at

status
```

Boas práticas:

- snake_case;
- nomes descritivos;
- evitar abreviações.

---

# Chaves Primárias

Todas as entidades utilizam UUID.

Exemplo:

```
id UUID PRIMARY KEY
```

Benefícios:

- maior segurança;
- menor previsibilidade;
- fácil integração entre serviços;
- escalabilidade para microsserviços.

Esta decisão está documentada no ADR-003.

---

# Relacionamentos

Os relacionamentos seguem as práticas do modelo relacional.

Exemplo:

```
Category

1

↓

N

Product
```

Uma categoria pode possuir vários produtos.

---

# Integridade Referencial

Sempre utilizar Foreign Keys.

Exemplo.

```
product.category_id

↓

category.id
```

Isso garante consistência dos dados.

---

# Evolução do Banco

Toda alteração estrutural deve ocorrer através de migrations.

Fluxo:

```
Nova necessidade

↓

Nova migration

↓

Commit

↓

Code Review

↓

Execução automática

↓

Banco atualizado
```

Nunca alterar tabelas manualmente.

---

# Flyway

O Atlas Commerce utiliza Flyway para versionamento do banco.

Na inicialização da aplicação:

```
Spring Boot

↓

Flyway

↓

Verifica versões

↓

Executa migrations

↓

Banco atualizado
```

Isso garante que todos os ambientes permaneçam sincronizados.

---

# Índices

Criar índices apenas quando necessário.

Exemplo:

```
CREATE INDEX idx_category_name
```

Objetivos:

- acelerar consultas;
- melhorar desempenho;
- reduzir tempo de resposta.

Evitar índices desnecessários.

---

# Tipos de Dados

Preferir tipos específicos.

Exemplos:

```
UUID

VARCHAR

TEXT

BOOLEAN

TIMESTAMP

NUMERIC

INTEGER
```

Evitar tipos genéricos sempre que possível.

---

# Auditoria

Todas as entidades persistentes deverão possuir campos de auditoria.

```
created_at

updated_at

deleted_at
```

Esses campos facilitam rastreabilidade e manutenção.

---

# Fluxo de Persistência

```
Controller

↓

Service

↓

Repository

↓

Hibernate

↓

PostgreSQL

↓

Repository

↓

Service

↓

Response
```

Esse fluxo garante separação de responsabilidades.

---

# Backup

Em ambientes produtivos, o banco deve possuir rotina automática de backup.

Fluxo recomendado:

```
Banco

↓

Backup diário

↓

Armazenamento seguro

↓

Validação periódica

↓

Recuperação quando necessário
```

---

# Segurança

Boas práticas:

- utilizar usuários específicos;
- princípio do menor privilégio;
- senhas fortes;
- conexões autenticadas;
- acesso restrito.

Nunca utilizar o usuário administrador na aplicação.

---

# O que NÃO fazer

Nunca:

- alterar tabelas manualmente;
- editar migrations já executadas;
- remover colunas sem migration;
- armazenar senhas em texto puro;
- utilizar tipos inadequados.

---

# Boas Práticas

✔ Utilizar UUID como chave primária.

✔ Versionar todas as alterações.

✔ Utilizar Foreign Keys.

✔ Nomear tabelas de forma consistente.

✔ Criar índices apenas quando necessário.

✔ Utilizar migrations pequenas.

✔ Documentar mudanças estruturais.

✔ Revisar impacto antes de alterar o banco.

---

# Benefícios

Essa arquitetura proporciona:

- consistência dos dados;
- facilidade de manutenção;
- evolução controlada;
- integração simplificada;
- alta confiabilidade;
- escalabilidade.

---

# Relação com Outros Documentos

Este documento complementa:

- deployment.md
- docker.md
- database-architecture.md
- ADR-001 — PostgreSQL
- ADR-003 — UUID

---

# Decisão Arquitetural

As decisões apresentadas neste documento estão formalizadas nos seguintes ADRs:

- ADR-001 — PostgreSQL
- ADR-003 — UUID
- ADR-004 — Repository Pattern

---

# Referências

- PostgreSQL Documentation
- Spring Data JPA
- Hibernate ORM
- Flyway Documentation
- SQL Standard

---

# Próximo Capítulo

deployment/environments.md