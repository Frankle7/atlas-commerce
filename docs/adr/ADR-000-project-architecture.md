# ADR-000 — Project Architecture

## Status

Accepted

---

## Objetivo

Definir a arquitetura geral do Atlas Commerce e estabelecer os princípios que orientarão a evolução técnica do projeto.

---

## Contexto

O Atlas Commerce é uma plataforma de e-commerce desenvolvida com foco em:

- organização
- escalabilidade
- manutenção
- testabilidade
- separação de responsabilidades
- boas práticas de engenharia de software

O projeto será desenvolvido incrementalmente através de missões, sprints e Features.

Por esse motivo, é necessário estabelecer uma arquitetura comum antes da implementação dos principais domínios de negócio.

---

## Problema

Sem uma arquitetura definida, cada módulo poderia adotar estruturas e padrões diferentes.

Isso poderia resultar em:

- alto acoplamento
- responsabilidades misturadas
- dificuldade de manutenção
- dificuldade de testes
- inconsistência entre módulos
- aumento do custo de evolução

---

## Decisão

O Atlas Commerce adotará uma arquitetura modular orientada a domínio, utilizando organização **Package by Feature**.

Cada domínio deverá concentrar seus componentes dentro de seu próprio módulo.

Exemplo:

```text
category/
├── controller/
├── dto/
├── entity/
├── mapper/
├── repository/
├── service/
├── specification/
└── validator/