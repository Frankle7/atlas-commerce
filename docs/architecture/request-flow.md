# Fluxo de Requisição

# Objetivo

Explicar detalhadamente como uma requisição HTTP percorre todas as camadas do Atlas Commerce, desde o momento em que é enviada pelo cliente até o retorno da resposta.

Este documento permite compreender como os componentes da aplicação trabalham em conjunto, facilitando o desenvolvimento, a depuração de erros e a evolução do sistema.

---

# Contexto

Toda interação com o Atlas Commerce acontece através de uma requisição HTTP.

Mesmo uma operação simples, como listar categorias, percorre diversas camadas internas antes de retornar uma resposta ao cliente.

Compreender esse fluxo é essencial para manter uma arquitetura organizada e evitar violações de responsabilidade entre as camadas.

---

# Motivação

Sem conhecer o fluxo completo da aplicação é comum encontrar problemas como:

- regras de negócio implementadas no Controller;
- acesso direto ao banco pela camada HTTP;
- duplicação de validações;
- dificuldade para localizar erros;
- baixo desacoplamento.

Este documento define o fluxo oficial adotado pelo projeto.

---

# Visão Geral

Toda requisição segue exatamente o mesmo caminho.

```
Cliente

↓

HTTP Request

↓

Controller

↓

Validação

↓

Service

↓

Repository

↓

PostgreSQL

↓

Repository

↓

Service

↓

Mapper

↓

DTO Response

↓

Controller

↓

HTTP Response

↓

Cliente
```

Independentemente do recurso acessado (`Category`, `Product`, `Order`, `User`, etc.), o fluxo permanece o mesmo.

---

# Etapa 1 — Cliente

O fluxo inicia quando um cliente realiza uma chamada HTTP.

O cliente pode ser:

- Aplicação Web
- Aplicação Mobile
- Sistema Externo
- Ferramentas como Postman ou Insomnia

Exemplo:

```
GET /api/v1/categories
```

---

# Etapa 2 — Controller

O Controller é o ponto de entrada da aplicação.

Suas responsabilidades são:

- receber a requisição;
- validar parâmetros básicos;
- encaminhar a operação para o Service;
- retornar a resposta.

O Controller nunca implementa regras de negócio.

```
Cliente

↓

CategoryController
```

---

# Etapa 3 — Validação

Antes da lógica de negócio ser executada, a aplicação valida os dados recebidos.

As validações podem ocorrer através de:

- Bean Validation
- Validators do domínio
- Conversão de DTOs

Exemplos:

- campos obrigatórios;
- tamanho máximo;
- formato de e-mail;
- UUID válido.

Caso exista alguma inconsistência, o fluxo é interrompido.

```
Request

↓

Validation

↓

Erro 400
```

---

# Etapa 4 — Service

Após a validação, o Controller delega a operação ao Service.

O Service concentra toda a lógica de negócio.

Exemplos:

- verificar duplicidade;
- validar regras comerciais;
- calcular valores;
- iniciar transações;
- orquestrar chamadas.

```
CategoryController

↓

CategoryService
```

---

# Etapa 5 — Repository

Quando é necessário acessar o banco de dados, o Service utiliza um Repository.

O Repository possui apenas responsabilidades relacionadas à persistência.

Exemplos:

```
save()

findById()

findAll()

delete()

existsByName()
```

Nenhuma regra de negócio deve existir nesta camada.

---

# Etapa 6 — Banco de Dados

O Repository comunica-se com o PostgreSQL utilizando Spring Data JPA.

Toda persistência é realizada através das Entities.

```
CategoryRepository

↓

PostgreSQL
```

---

# Etapa 7 — Retorno da Persistência

Após a execução da operação no banco, o Repository devolve o resultado ao Service.

O Service ainda pode:

- aplicar regras adicionais;
- lançar exceções;
- transformar entidades;
- preparar a resposta.

---

# Etapa 8 — Conversão para DTO

As Entities nunca são expostas diretamente para o cliente.

Antes da resposta ser enviada, os dados são convertidos para DTOs.

```
Category

↓

CategoryMapper

↓

CategoryResponse
```

Essa separação reduz acoplamento e preserva o contrato da API.

---

# Etapa 9 — Resposta HTTP

O Controller recebe o DTO de resposta e devolve um objeto HTTP ao cliente.

Exemplo:

```json
{
  "id": "5c5e7c9b-94cf-42f6-9db6-f3c3d4bb8d63",
  "name": "Electronics"
}
```

---

# Fluxo Completo

```
Cliente

↓

HTTP Request

↓

Controller

↓

DTO Request

↓

Validator

↓

Service

↓

Repository

↓

PostgreSQL

↓

Repository

↓

Service

↓

Mapper

↓

DTO Response

↓

Controller

↓

HTTP Response

↓

Cliente
```

---

# Tratamento de Erros

Durante qualquer etapa do fluxo podem ocorrer exceções.

Exemplos:

```
ValidationException

↓

400 Bad Request
```

```
CategoryNotFoundException

↓

404 Not Found
```

```
DuplicateCategoryException

↓

409 Conflict
```

As exceções são tratadas globalmente pelo mecanismo de tratamento de erros da aplicação.

---

# Benefícios do Fluxo

A separação clara entre camadas proporciona:

- alta coesão;
- baixo acoplamento;
- facilidade de testes;
- manutenção simplificada;
- reutilização de código;
- evolução segura.

---

# Boas Práticas

- Nunca acessar o Repository diretamente pelo Controller.
- Nunca implementar regras de negócio na camada HTTP.
- Utilizar DTOs para comunicação externa.
- Centralizar validações.
- Delegar toda lógica ao Service.
- Retornar respostas padronizadas.

---

# Erros Comuns

- Controller acessando Repository.
- Service retornando Entity diretamente.
- Validação duplicada em múltiplas camadas.
- Conversões espalhadas pelo código.
- Exceções tratadas manualmente em cada Controller.

---

# Decisão Arquitetural

Este fluxo implementa as decisões definidas em:

- ADR-000 — Arquitetura Geral
- ADR-004 — Repository Pattern
- ADR-005 — Package by Feature

---

# Referências

Spring MVC

Spring Boot Reference

Spring Data JPA

Jakarta Bean Validation

RESTful Web Services

---

# Próximo Capítulo

module-diagram.md