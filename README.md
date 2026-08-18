# Desafio Tech Lead — Reserva de Salas de Reunião

Monorepo do desafio: uma aplicação de **reserva de salas de reunião**, com
back-end (API REST) e front-end (cliente web) versionados como **git
submodules**, orquestrados juntos via Docker Compose.

- [`desafio_techlead_back`](desafio_techlead_back/) — API NestJS + Prisma +
  PostgreSQL, com autenticação JWT e controle de acesso por papel
  (`USER`/`ADMIN`). Gerencia usuários, salas e reservas.
- [`desafio_techlead_front`](desafio_techlead_front/) — Cliente Next.js/React
  que consome a API acima.

Detalhes de stack, modelo de dados e endpoints estão nos READMEs de cada
submódulo — este arquivo cobre só a visão geral e como subir tudo junto.

## Como rodar com Docker

Pré-requisito: Docker + Docker Compose.

1. Clone o repositório trazendo os submódulos:

   ```bash
   git clone --recurse-submodules <url-do-repositorio>
   ```

   Se já clonou sem essa flag:

   ```bash
   git submodule update --init --recursive
   ```

2. Crie um `.env` na raiz do projeto com as credenciais do banco:

   ```
   POSTGRES_USER=usuario
   POSTGRES_PASSWORD=senha
   POSTGRES_DB=nome_do_banco
   ```

3. Suba os containers:

   ```bash
   docker compose up --build
   ```

Isso sobe três serviços:

| Serviço    | Container             | Porta  |
| ---------- | ---------------------- | ------ |
| `db`       | `booking_db` (Postgres) | 5432   |
| `backend`  | `desafio_techlead_back` | 3000   |
| `frontend` | `desagio_techlead_front`| 3001   |

A ordem de subida é `db` → `backend` → `frontend` (via `depends_on`).
