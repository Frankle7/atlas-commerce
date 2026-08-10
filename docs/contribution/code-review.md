# Code Review

---

# Objetivo

Definir o processo oficial de Code Review utilizado no Atlas Commerce.

Este documento estabelece como toda alteração deve ser analisada antes de ser integrada ao projeto, garantindo qualidade, padronização e evolução contínua da base de código.

Ao concluir este capítulo, o desenvolvedor compreenderá como revisar código de forma técnica, objetiva e colaborativa.

---

# Contexto

Escrever código é apenas parte do desenvolvimento de software.

Antes que qualquer alteração seja incorporada ao projeto, ela deve passar por uma revisão.

O Code Review é uma das principais práticas utilizadas por equipes de alta performance para reduzir erros, compartilhar conhecimento e manter a qualidade do código ao longo do tempo.

No Atlas Commerce, nenhuma Feature é considerada concluída sem passar pelo processo de revisão.

---

# Motivação

O objetivo do Code Review não é encontrar culpados.

Seu propósito é melhorar o software.

Entre os principais benefícios estão:

- redução de bugs;
- compartilhamento de conhecimento;
- padronização do código;
- melhoria contínua da arquitetura;
- prevenção de regressões;
- fortalecimento da cultura técnica da equipe.

Cada revisão representa uma oportunidade de aprendizado.

---

# Fluxo Oficial

Todo desenvolvimento segue o fluxo abaixo.

```
Nova Feature

↓

Implementação

↓

Commits

↓

Push

↓

Pull Request

↓

Code Review

↓

Correções (se necessário)

↓

Aprovação

↓

Merge

↓

Sprint
```

Nenhuma Feature deve ser integrada diretamente sem revisão.

---

# Processo de Revisão

O revisor deve analisar a alteração considerando diferentes aspectos da aplicação.

O objetivo não é apenas verificar se o código funciona, mas se ele atende aos padrões definidos pelo projeto.

A revisão deve responder perguntas como:

- O código resolve corretamente o problema?
- Está seguindo a arquitetura?
- Está fácil de entender?
- Está consistente com o restante do projeto?
- Existe uma solução mais simples?

---

# Checklist Oficial

Antes de aprovar um Pull Request, o revisor deve verificar os seguintes itens.

## Arquitetura

- segue Package by Feature;
- respeita as camadas da aplicação;
- não quebra a Clean Architecture;
- utiliza os módulos corretos.

---

## Código

- nomes claros;
- métodos pequenos;
- classes coesas;
- ausência de duplicação;
- responsabilidades bem definidas.

---

## Controllers

Verificar se:

- não possuem regras de negócio;
- retornam DTOs;
- utilizam códigos HTTP corretos;
- delegam responsabilidades para a Service.

---

## Services

Verificar se:

- concentram as regras de negócio;
- não possuem código duplicado;
- utilizam Validators quando necessário;
- acessam dados apenas pelos Repositories.

---

## Repositories

Verificar se:

- utilizam Spring Data JPA;
- possuem consultas organizadas;
- não contêm lógica de negócio.

---

## DTOs

Verificar se:

- representam corretamente contratos da API;
- não expõem entidades;
- possuem apenas os campos necessários.

---

## Mappers

Verificar se:

- realizam apenas conversões;
- não possuem regras de negócio;
- são reutilizáveis.

---

## Validators

Verificar se:

- encapsulam validações específicas do domínio;
- evitam sobrecarregar a Service;
- possuem responsabilidade única.

---

## Banco de Dados

Quando houver alterações no banco, verificar:

- migrations versionadas;
- nomenclatura consistente;
- compatibilidade com versões anteriores;
- impacto em produção.

---

## API

Verificar se:

- endpoints seguem REST;
- respostas seguem o padrão oficial;
- erros utilizam Error Pattern;
- paginação segue o padrão do projeto.

---

## Testes

Toda Feature deve possuir testes quando aplicável.

Verificar:

- testes unitários;
- testes de integração;
- cobertura das regras críticas;
- cenários de erro.

---

# Perguntas Durante a Revisão

Um bom revisor costuma fazer perguntas como:

- Este código pode ser simplificado?
- Existe duplicação?
- O nome está adequado?
- A responsabilidade está correta?
- Há risco de regressão?
- O código será fácil de manter daqui a um ano?

---

# Comentários de Review

Os comentários devem ser claros, técnicos e respeitosos.

Bom exemplo:

```
Sugestão:

Podemos mover esta validação para o Validator.

Assim mantemos a Service responsável apenas pelas regras de negócio.
```

Evite comentários vagos como:

```
Está estranho.

Melhorar isso.

Não gostei.
```

Toda sugestão deve explicar o motivo.

---

# Critérios de Aprovação

Um Pull Request pode ser aprovado quando:

- arquitetura respeitada;
- padrão de código seguido;
- documentação atualizada;
- testes executados;
- build funcionando;
- sem conflitos;
- checklist concluído.

---

# Critérios para Solicitar Alterações

O revisor deve solicitar mudanças quando encontrar:

- regras de negócio em Controllers;
- duplicação de código;
- violações da arquitetura;
- ausência de testes;
- nomes inadequados;
- baixa legibilidade;
- riscos para produção.

---

# Exemplo de Fluxo

```
Feature/missao-004

↓

Commits

↓

Push

↓

Pull Request

↓

Reviewer

↓

Comentários

↓

Correções

↓

Nova revisão

↓

Aprovado

↓

Merge na Sprint
```

---

# Relação com o Git Workflow

No Atlas Commerce, o fluxo padrão é:

```
main

↓

sprint-001

↓

feature/missao-004

↓

Pull Request

↓

Code Review

↓

Merge

↓

Sprint

↓

Release

↓

main
```

O Code Review é a etapa que garante a qualidade antes da integração.

---

# Ferramentas Utilizadas

Durante a revisão podem ser utilizadas ferramentas como:

- GitHub Pull Requests;
- Git Diff;
- IntelliJ IDEA;
- VS Code;
- SonarQube (futuramente);
- Checkstyle (futuramente).

---

# O que NÃO fazer

Nunca:

- aprovar sem revisar;
- revisar apenas a formatação;
- ignorar testes;
- alterar código diretamente na branch de outro desenvolvedor;
- aprovar código que viola a arquitetura;
- transformar a revisão em uma discussão pessoal.

O foco sempre deve ser o código.

---

# Boas Práticas

✔ Revisar pequenas alterações.

✔ Explicar todas as sugestões.

✔ Questionar decisões técnicas.

✔ Manter uma comunicação respeitosa.

✔ Incentivar aprendizado.

✔ Revisar arquitetura antes da implementação.

✔ Verificar impacto da alteração.

✔ Confirmar aderência aos ADRs.

---

# Benefícios

Seguindo este processo, o Atlas Commerce obtém:

- maior qualidade do código;
- menor quantidade de bugs;
- compartilhamento contínuo de conhecimento;
- evolução consistente da arquitetura;
- histórico mais confiável;
- onboarding facilitado;
- manutenção mais simples.

---

# Decisão Arquitetural

Este processo está alinhado com:

- ADR-000 — Arquitetura Geral
- ADR-004 — Repository Pattern
- ADR-005 — Package by Feature
- Git Workflow
- Conventional Commits

---

# Referências

- GitHub Code Review Guidelines
- Google Engineering Practices
- Microsoft Engineering Playbook
- Clean Code
- Clean Architecture
- Domain-Driven Design

---

# Próximo Capítulo

contribution/contribution.md