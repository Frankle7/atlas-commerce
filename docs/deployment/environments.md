# Environments

---

# Objetivo

Definir a estratégia oficial de gerenciamento de ambientes do Atlas Commerce.

Este documento apresenta os diferentes ambientes utilizados durante o ciclo de vida da aplicação, suas responsabilidades, configurações, boas práticas e fluxo de promoção entre eles.

Ao final deste capítulo, qualquer desenvolvedor deverá compreender onde desenvolver, testar, validar e publicar novas funcionalidades de forma segura.

---

# Contexto

Uma aplicação profissional nunca possui apenas um ambiente.

Durante seu desenvolvimento o software passa por diversas etapas até chegar ao usuário final.

Cada ambiente possui objetivos diferentes, níveis distintos de estabilidade e configurações específicas.

Separar corretamente esses ambientes reduz riscos, aumenta a confiabilidade e evita que mudanças em desenvolvimento afetem usuários reais.

---

# Motivação

Imagine desenvolver diretamente no ambiente de produção.

Qualquer erro pode:

- derrubar a aplicação;
- corromper dados;
- causar indisponibilidade;
- impactar clientes.

Por esse motivo utilizamos múltiplos ambientes.

Cada um possui uma finalidade específica.

---

# Ambientes Oficiais

O Atlas Commerce utiliza quatro ambientes principais.

```
Developer

↓

Development

↓

Staging

↓

Production
```

Cada ambiente representa uma etapa da evolução do software.

---

# Development

O ambiente de Development é utilizado pelos desenvolvedores durante a implementação das funcionalidades.

Características:

- ambiente local;
- Docker;
- PostgreSQL local;
- logs detalhados;
- dados fictícios;
- alterações constantes.

Objetivo principal:

Desenvolver novas funcionalidades.

---

# Staging

O ambiente de Staging representa uma cópia quase idêntica da Produção.

Objetivos:

- validar deploy;
- executar testes integrados;
- validar migrations;
- realizar testes manuais.

Nenhuma funcionalidade deve ser enviada para Produção sem passar pelo Staging.

---

# Production

Production é o ambiente utilizado pelos usuários finais.

Características:

- alta disponibilidade;
- monitoramento;
- backups automáticos;
- segurança reforçada;
- logs controlados;
- dados reais.

Toda alteração neste ambiente deve seguir o fluxo oficial de aprovação.

---

# Fluxo entre Ambientes

```
Feature Branch

↓

Sprint

↓

Main

↓

Build

↓

Development

↓

Staging

↓

Production
```

Esse fluxo garante que toda alteração seja validada antes da publicação.

---

# Configuração por Ambiente

Cada ambiente possui configurações próprias.

Exemplo:

```
application.yml

application-dev.yml

application-stage.yml

application-prod.yml
```

Nunca utilizar uma única configuração para todos os ambientes.

---

# Variáveis de Ambiente

Informações sensíveis nunca devem ser armazenadas no código.

Exemplos:

```
DATABASE_URL

DATABASE_USER

DATABASE_PASSWORD

JWT_SECRET

SMTP_PASSWORD

REDIS_HOST
```

Esses valores devem ser fornecidos através de variáveis de ambiente.

---

# Arquivo .env

Durante o desenvolvimento utilizamos um arquivo `.env`.

Exemplo:

```env
POSTGRES_DB=atlas

POSTGRES_USER=postgres

POSTGRES_PASSWORD=postgres

JWT_SECRET=my-secret
```

O arquivo `.env` nunca deve conter credenciais de produção.

---

# Configuração do Spring Boot

O Spring Boot seleciona automaticamente o ambiente ativo.

Exemplo:

```bash
SPRING_PROFILES_ACTIVE=dev
```

Outros perfis:

```
dev

stage

prod
```

Cada perfil possui configurações independentes.

---

# Banco de Dados

Cada ambiente deve possuir seu próprio banco.

```
Development

↓

atlas_dev

-----------------

Staging

↓

atlas_stage

-----------------

Production

↓

atlas_prod
```

Nunca compartilhar o mesmo banco entre ambientes.

---

# Migrations

As migrations são executadas automaticamente pelo Flyway.

Fluxo:

```
Nova Migration

↓

Commit

↓

Deploy

↓

Flyway

↓

Banco Atualizado
```

Todos os ambientes permanecem sincronizados.

---

# Logs

Cada ambiente possui uma política diferente de logs.

Development

- logs completos;
- stack traces;
- SQL exibido.

Staging

- logs moderados;
- validações.

Production

- logs controlados;
- monitoramento;
- auditoria.

---

# Dados Utilizados

Development

- dados fictícios.

Staging

- dados anonimizados ou simulados.

Production

- dados reais.

Nunca copiar dados sensíveis para ambientes de desenvolvimento.

---

# Segurança

Cada ambiente possui níveis distintos de acesso.

```
Developer

↓

Development

↓

Staging

↓

Production
```

Quanto mais próximo da produção, maior o nível de controle.

---

# Processo de Deploy

```
Commit

↓

Pull Request

↓

Code Review

↓

Merge

↓

Pipeline

↓

Deploy Development

↓

Deploy Staging

↓

Deploy Production
```

Nenhum deploy deve ocorrer manualmente em produção.

---

# Monitoramento

Após cada deploy, a aplicação deve ser monitorada.

Itens importantes:

- disponibilidade;
- consumo de memória;
- uso de CPU;
- tempo de resposta;
- erros HTTP;
- logs.

---

# Recuperação

Caso um deploy apresente falhas:

```
Deploy

↓

Erro

↓

Rollback

↓

Versão Estável
```

Todo ambiente deve possuir estratégia de rollback.

---

# O que NÃO fazer

Nunca:

- utilizar banco de produção para testes;
- compartilhar credenciais;
- armazenar segredos no Git;
- modificar produção manualmente;
- realizar testes diretamente em produção.

---

# Boas Práticas

✔ Utilizar perfis separados.

✔ Configurações independentes.

✔ Variáveis de ambiente.

✔ Deploy automatizado.

✔ Banco exclusivo por ambiente.

✔ Backup antes de deploy.

✔ Rollback documentado.

✔ Monitoramento contínuo.

---

# Benefícios

Essa estratégia proporciona:

- maior segurança;
- previsibilidade;
- estabilidade;
- facilidade de manutenção;
- menor risco operacional;
- implantação controlada.

---

# Relação com Outros Documentos

Este documento complementa:

- deployment.md
- docker.md
- postgres.md
- ci-cd.md
- development-environment.md

---

# Decisão Arquitetural

As decisões relacionadas aos ambientes estão alinhadas com:

- ADR-000 — Arquitetura Geral
- ADR-001 — PostgreSQL
- ADR-002 — JWT
- ADR-004 — Repository Pattern

---

# Referências

- Spring Boot Profiles
- Docker Documentation
- Twelve-Factor App
- Flyway Documentation
- PostgreSQL Documentation

---

# Próximo Capítulo

deployment/ci-cd.md