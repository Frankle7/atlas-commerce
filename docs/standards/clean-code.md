# Clean Code

## Objetivo

Definir os princípios de Clean Code adotados pelo Atlas Commerce, estabelecendo um padrão de escrita que prioriza legibilidade, simplicidade, manutenção e evolução contínua do software.

Este documento não apresenta apenas regras, mas explica a filosofia por trás de um código limpo e como ela influencia a arquitetura do projeto.

---

# Contexto

Escrever código que funcione é relativamente simples.

Escrever código que permaneça compreensível após anos de evolução é um desafio muito maior.

Em projetos corporativos, o código é lido muito mais vezes do que é escrito.

Por esse motivo, cada linha deve ser pensada para facilitar a vida do próximo desenvolvedor.

---

# Motivação

O Atlas Commerce é um projeto de longo prazo.

Ao longo do tempo:

- novas funcionalidades serão adicionadas;
- desenvolvedores entrarão e sairão da equipe;
- regras de negócio mudarão;
- módulos crescerão continuamente.

Sem um padrão consistente, o sistema rapidamente se torna difícil de entender e manter.

Nosso objetivo é construir um software que continue simples mesmo após centenas de commits.

---

# Filosofia

No Atlas Commerce seguimos alguns princípios fundamentais.

```
Código é escrito para pessoas.

↓

Computadores apenas executam.
```

```
Legibilidade

>

Complexidade
```

```
Simplicidade

>

Criatividade
```

```
Consistência

>

Preferência pessoal
```

Sempre escolha a solução mais simples que resolva corretamente o problema.

---

# O que é Clean Code?

Código limpo é aquele que:

- possui nomes claros;
- possui pequenas responsabilidades;
- é previsível;
- é fácil de modificar;
- possui baixa complexidade;
- possui poucos efeitos colaterais.

Uma pessoa deve conseguir compreender uma classe poucos minutos após abri-la.

---

# A Regra do Escoteiro

Inspirada por Robert C. Martin.

> "Sempre deixe o código um pouco melhor do que você encontrou."

Não é necessário realizar grandes refatorações.

Pequenas melhorias constantes geram enorme qualidade ao longo do tempo.

Exemplos:

- melhorar um nome;
- remover código morto;
- organizar imports;
- eliminar duplicação;
- simplificar um método.

---

# Nomes Claros

Nomes devem revelar intenção.

Evite abreviações.

✔ Bom

```java
CategoryRepository

CategoryService

findCategoryById()
```

❌ Ruim

```java
CatRepo

Srv

exec()
```

Quem lê o código não deve precisar adivinhar o significado.

---

# Uma Classe, Uma Responsabilidade

Cada classe deve resolver apenas um problema.

Exemplo correto:

```
CategoryController

↓

Receber requisições
```

```
CategoryService

↓

Executar regras de negócio
```

```
CategoryRepository

↓

Persistência
```

Misturar responsabilidades aumenta acoplamento e dificulta testes.

---

# Métodos Pequenos

Métodos devem possuir uma única responsabilidade.

Idealmente:

- até 20~30 linhas;
- poucos parâmetros;
- fácil leitura.

✔

```java
createCategory()
```

❌

```java
createCategoryAndValidateAndSaveAndNotify()
```

Se o nome do método contém "And", provavelmente existem responsabilidades demais.

---

# Evite Comentários Desnecessários

Comentários não substituem código ruim.

Ruim:

```java
// incrementa contador

count++;
```

Bom:

```java
processedItems++;
```

Comentários devem explicar decisões arquiteturais, nunca código óbvio.

---

# Evite Código Duplicado

Duplicação aumenta custo de manutenção.

Sempre que identificar lógica repetida:

- extraia um método;
- reutilize componentes;
- utilize abstrações.

---

# Evite Métodos Gigantes

Métodos longos escondem responsabilidades.

Ruim:

```
Método

↓

300 linhas
```

Bom:

```
Controller

↓

Service

↓

Validator

↓

Repository
```

Cada etapa possui responsabilidade específica.

---

# Evite Classes Gigantes

Uma classe enorme normalmente indica que ela está fazendo trabalho demais.

Se uma classe cresce continuamente, considere dividi-la.

Sinais de alerta:

- centenas de linhas;
- muitos atributos;
- muitos métodos públicos;
- múltiplas responsabilidades.

---

# Evite Booleanos Confusos

Ruim:

```java
process(true, false, true);
```

Bom:

```java
processPayment(
    validateStock,
    sendNotification,
    generateInvoice
);
```

Parâmetros devem ser autoexplicativos.

---

# Evite Números Mágicos

Nunca escreva valores sem contexto.

Ruim:

```java
if(pageSize > 100)
```

Bom:

```java
private static final int MAX_PAGE_SIZE = 100;
```

---

# Reduza o Acoplamento

Classes devem conhecer apenas o necessário.

Ruim:

```
Controller

↓

Repository
```

Bom:

```
Controller

↓

Service

↓

Repository
```

---

# Prefira Composição

Sempre que possível:

```
Composição

>

Herança
```

Composição gera código mais flexível e desacoplado.

---

# Falhe Rapidamente (Fail Fast)

Erros devem ser detectados o mais cedo possível.

Exemplo:

```java
Objects.requireNonNull(category);
```

Validar entradas evita erros mais difíceis de rastrear.

---

# Tratamento de Exceções

Nunca capture exceções apenas para ignorá-las.

Ruim:

```java
catch(Exception e){}
```

Bom:

```java
throw new CategoryNotFoundException(id);
```

Exceções devem comunicar claramente o problema.

---

# Código Morto

Código não utilizado deve ser removido.

Evite:

- métodos comentados;
- classes abandonadas;
- TODOs antigos;
- imports não utilizados.

O histórico do Git preserva versões antigas.

---

# Organização Visual

Código bem organizado facilita leitura.

Exemplo:

```java
Atributos

↓

Construtores

↓

Métodos Públicos

↓

Métodos Privados
```

Mantenha espaçamento consistente.

---

# Refatoração Contínua

Refatoração não é uma atividade isolada.

Ela faz parte do desenvolvimento diário.

Sempre que modificar um trecho de código:

- simplifique;
- renomeie;
- elimine duplicações;
- reduza complexidade.

---

# Sinais de Código Ruim

Os principais "code smells" incluem:

- métodos enormes;
- classes gigantes;
- duplicação;
- nomes genéricos;
- excesso de parâmetros;
- comentários explicando código simples;
- condicionais complexas;
- dependências excessivas.

Sempre que identificar um desses sinais, avalie a necessidade de refatoração.

---

# Fluxo de Desenvolvimento

```
Implementar

↓

Revisar

↓

Simplificar

↓

Refatorar

↓

Testar

↓

Documentar

↓

Commit
```

Código limpo nasce durante o desenvolvimento, não apenas ao final.

---

# Checklist de Clean Code

Antes de concluir uma implementação, confirme:

- Os nomes são claros?
- Existe apenas uma responsabilidade por classe?
- Os métodos são pequenos?
- Há duplicação?
- O código é fácil de entender?
- Existem comentários desnecessários?
- Os testes continuam passando?
- Há alguma refatoração simples que pode ser feita?

---

# Boas Práticas

- Escreva código para pessoas.
- Prefira simplicidade.
- Utilize nomes descritivos.
- Extraia responsabilidades.
- Elimine duplicação.
- Refatore continuamente.
- Mantenha métodos pequenos.
- Faça pequenas melhorias em cada alteração.

---

# Erros Comuns

- Classes enormes.
- Métodos gigantes.
- Nomes genéricos.
- Comentários desnecessários.
- Código duplicado.
- Alto acoplamento.
- Ignorar refatorações.
- Complexidade desnecessária.

---

# Relação com Outros Documentos

- standards/coding-standards.md
- standards/naming.md
- standards/package-structure.md
- contribution/code-review.md
- architecture/package-architecture.md

---

# Referências

- Clean Code — Robert C. Martin
- Clean Architecture — Robert C. Martin
- Refactoring — Martin Fowler
- Effective Java — Joshua Bloch

---

# Próximo Capítulo

naming.md