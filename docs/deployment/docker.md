# Docker

---

# Objetivo

Definir o padrão oficial de utilização do Docker no Atlas Commerce.

Este documento explica por que utilizamos containers, como a infraestrutura foi organizada e como executar todo o ambiente de desenvolvimento utilizando Docker.

---

# Contexto

Uma das maiores dificuldades em equipes de desenvolvimento é garantir que todos trabalhem exatamente no mesmo ambiente.

Diferenças de sistema operacional, versões de banco de dados, configurações locais e dependências costumam gerar erros difíceis de reproduzir.

O Docker elimina esse problema criando ambientes isolados e reproduzíveis.

---

# Motivação

Antes do Docker era comum encontrar problemas como:

- Funciona apenas na minha máquina;
- Banco em versão diferente;
- Dependências incompatíveis;
- Configurações manuais;
- Horas perdidas configurando ambiente.

Com containers todo desenvolvedor utiliza exatamente a mesma infraestrutura.

---

# O que é Docker

Docker é uma plataforma de virtualização leve baseada em containers.

Ao invés de instalar todos os serviços diretamente no computador, eles são executados isoladamente.

```
Notebook

│

├── Docker

│

├── PostgreSQL

├── Redis

├── RabbitMQ

└── Outros Serviços
```

Cada serviço funciona independentemente.

---

# Arquitetura do Atlas Commerce

```
               Atlas Commerce

                     │

      ┌──────────────┴──────────────┐

      │                             │

 Spring Boot                  PostgreSQL

      │                             │

      └──────────────┬──────────────┘

                     │

               Docker Compose
```

Docker Compose é responsável por iniciar toda a infraestrutura.

---

# Estrutura

```
docker/

└── postgres/
    ├── Dockerfile
    ├── postgres.conf
    └── init/

docker-compose.yml
```

Cada pasta possui responsabilidade específica.

---

# Dockerfile

O Dockerfile define como uma imagem será construída.

Exemplo simplificado:

```dockerfile
FROM postgres:17

COPY postgres.conf /etc/postgresql/

COPY init/ /docker-entrypoint-initdb.d/
```

Sempre que um container é criado, essa configuração é aplicada automaticamente.

---

# Docker Compose

O Docker Compose define quais containers fazem parte do ambiente.

Exemplo:

```yaml
services:

  postgres:

    image: postgres:17

    container_name: atlas-postgres

    ports:
      - "5432:5432"

    env_file:
      - .env
```

Um único comando sobe toda a infraestrutura.

---

# Inicializando os Containers

Subir ambiente.

```bash
docker compose up -d
```

Parar ambiente.

```bash
docker compose down
```

Reiniciar.

```bash
docker compose restart
```

---

# Verificando Containers

Listar containers ativos.

```bash
docker ps
```

Todos os containers.

```bash
docker ps -a
```

---

# Logs

Visualizar logs.

```bash
docker logs atlas-postgres
```

Acompanhar continuamente.

```bash
docker logs -f atlas-postgres
```

---

# Volumes

Os dados do PostgreSQL são armazenados em volumes.

```
Container

↓

Volume Docker

↓

Persistência
```

Mesmo removendo o container, os dados permanecem.

---

# Redes

Todos os containers compartilham uma rede privada criada automaticamente pelo Docker Compose.

```
Spring Boot

↓

Docker Network

↓

PostgreSQL
```

Isso elimina configurações complexas de rede.

---

# Fluxo de Inicialização

```
docker compose up

↓

Docker cria Network

↓

Docker cria Volumes

↓

PostgreSQL inicia

↓

Spring conecta

↓

Flyway executa

↓

API disponível
```

---

# Atualizando Containers

Quando houver alteração no Dockerfile:

```bash
docker compose build
```

Depois:

```bash
docker compose up -d
```

---

# Removendo Ambiente

Remover containers.

```bash
docker compose down
```

Remover containers e volumes.

```bash
docker compose down -v
```

Utilize com cuidado, pois os dados serão apagados.

---

# Problemas Comuns

## Porta ocupada

```
Port 5432 already in use
```

Verifique qual processo utiliza a porta.

---

## Container não inicia

Consultar logs.

```bash
docker logs atlas-postgres
```

---

## Banco inacessível

Verificar:

- Docker Desktop iniciado;
- Container ativo;
- Variáveis do `.env`;
- Porta 5432.

---

# O que NÃO fazer

Nunca:

- alterar containers manualmente;
- armazenar dados importantes dentro do container;
- utilizar senhas fixas no Dockerfile;
- modificar imagens oficiais diretamente.

---

# Boas Práticas

✔ Utilizar sempre Docker Compose.

✔ Versionar Dockerfile.

✔ Utilizar `.env`.

✔ Utilizar volumes.

✔ Isolar serviços.

✔ Manter containers pequenos.

✔ Reconstruir imagens sempre que necessário.

---

# Benefícios

O uso do Docker proporciona:

- ambiente padronizado;
- facilidade de instalação;
- isolamento;
- reprodutibilidade;
- menor tempo de onboarding;
- maior estabilidade.

---

# Relação com Outros Documentos

- deployment.md
- postgres.md
- environments.md
- ci-cd.md
- development-environment.md

---

# Referências

- Docker Documentation
- Docker Compose Documentation
- PostgreSQL Docker Image

---

# Próximo Capítulo

deployment/postgres.md