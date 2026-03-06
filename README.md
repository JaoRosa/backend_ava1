# AVA1 — Backend (Trabalho de Faculdade)

[![Status](https://img.shields.io/badge/status-pronto-brightgreen)](https://github.com/) [![Node](https://img.shields.io/badge/node-%3E=_14.x-green)](https://nodejs.org/)  
Backend responsável pela API, persistência e lógica do trabalho. Projeto feito para demonstrar arquitetura, autenticação, persistência e testes.

---

## Visão geral
Pequena descrição: API RESTful que expõe endpoints para CRUD das entidades, com autenticação JWT, validação, logs básicos e documentação (OpenAPI/Swagger). Objetivo: entregar um sistema funcional e testável para avaliação.

---

## Principais funcionalidades
- Registro e login com JWT + refresh tokens
- CRUD completo para entidades do sistema (ex.: usuários, cursos, tarefas)
- Validação de entrada e tratamento padronizado de erros
- Upload simples de arquivos (opcional)
- Paginação, ordenação e filtros nas listagens
- Scripts de migração e seed
- Testes automatizados (Jest + Supertest)
- Documentação de API (Swagger/OpenAPI)

---

## Tecnologias
- Node.js + Express (ou Fastify)
- ORM: Sequelize / TypeORM / Prisma
- PostgreSQL (produção) / SQLite (dev)
- Autenticação: JWT
- Testes: Jest + Supertest
- Docker + docker-compose (opcional)

---

## Quickstart (exemplo)
1. Clonar:
  git clone <url-do-repo>
2. Instalar:
  cd vue-backend
  npm install
3. Criar .env (ex.: DB, JWT_SECRET, PORT)
4. Migrar / seed:
  npm run migrate
5. Rodar em dev:
  npm run dev
6. Acessar:
  http://localhost:3000
(Adapte comandos conforme package manager e scripts do projeto.)

---

## Estrutura sugerida
- src/
  - controllers/
  - services/
  - repositories/
  - models/
  - routes/
  - middlewares/
  - config/
  - tests/
- migrations/
- docker-compose.yml
- .env.example

---

## Exemplos de uso (curl)
- Registrar:
  curl -X POST http://localhost:3000/auth/register -H "Content-Type: application/json" -d '{"email":"aluno@ex","password":"senha"}'
- Login:
  curl -X POST http://localhost:3000/auth/login -H "Content-Type: application/json" -d '{"email":"aluno@ex","password":"senha"}'
- Criar recurso (ex.: tarefa):
  curl -X POST http://localhost:3000/tasks -H "Authorization: Bearer <TOKEN>" -H "Content-Type: application/json" -d '{"title":"Trabalho","dueDate":"2026-04-01"}'

---

## Testes
- Rodar todos:
  npm test
- Testes E2E com Supertest cobrem fluxos críticos: autenticação, criação/edição/exclusão de entidades e respostas de erro.

---

## Boas práticas aplicadas
- Validação via schema (ex.: Joi / Zod)
- Tratamento centralizado de erros com códigos
