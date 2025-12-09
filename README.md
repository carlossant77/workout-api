# 🏋️ Workout API Challenge: Gestão de Atletas

<p align="center">
  <img src="https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=fastapi" />
  <img src="https://img.shields.io/badge/PostgreSQL-316192?style=for-the-badge&logo=postgresql&logoColor=white" />
  <img src="https://img.shields.io/badge/Python-3.11+-3776AB?style=for-the-badge&logo=python&logoColor=white" />
  <img src="https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white" />
</p>

## 🌟 Visão Geral

Este projeto é uma **API Assíncrona** de alta performance para gerenciamento de dados de treino e atletas. Desenvolvida com **FastAPI** e utilizando **SQLAlchemy 2.0** para persistência de dados em um banco **PostgreSQL**, a aplicação garante integridade de dados e consultas rápidas.

---

## 🚀 Guia de Início Rápido (Quick Start)

A maneira mais fácil de rodar a API é utilizando o Docker Compose, que gerencia tanto a aplicação FastAPI quanto o contêiner do banco de dados.

### 📋 Pré-requisitos

Certifique-se de que você tem instalado:
* **Docker** e **Docker Compose**
* **Git**

### 🐳 Rodando com Docker Compose

1.  **Clone o Repositório:**
    ```bash
    git clone [(https://github.com/carlossant77/workout-api)]
    cd workoutAPI
    ```

2.  **Inicie os Serviços:**
    Este comando irá construir a imagem da API, configurar o PostgreSQL e subir ambos os contêineres em segundo plano.
    ```bash
    docker-compose up --build -d
    ```

3.  **Verifique o Status:**
    Confirme se tudo está rodando corretamente:
    ```bash
    docker-compose ps
    # STATUS: api e db devem estar como "Up"
    ```
    ✅ A API estará disponível em `http://localhost:8000`.

---

## 🌐 Rotas e Documentação Interativa

Todas as rotas da API estão documentadas e prontas para teste através da interface Swagger UI.

| Link | Descrição |
| :--- | :--- |
| **Swagger UI (Recomendado)** | A documentação interativa para testar as rotas. |
| `http://localhost:8000/docs` | `http://localhost:8000/docs` |
| **Redoc** | Uma alternativa mais simples para visualização. |
| `http://localhost:8000/redoc` | `http://localhost:8000/redoc` |

### 🎯 Rotas Principais (Exemplos)

| Método | Caminho | Resumo |
| :--- | :--- | :--- |
| **POST** | `/categorias/` | ➕ Cria uma nova Categoria (Ex: Scale). |
| **POST** | `/atletas/` | 👤 Cadastra um novo Atleta. |
| **GET** | `/atletas/` | 🔍 Consulta todos os atletas com suporte a **Paginação** e **Filtros** (`?page=1&size=10`). |
| **PATCH** | `/atletas/{id}` | 📝 Edita dados de um atleta específico. |

---

## 🧩 Stack Tecnológico

As principais ferramentas e bibliotecas utilizadas neste projeto, com foco em performance e assincronicidade:

| Categoria | Pacote | Propósito |
| :--- | :--- | :--- |
| **API Web** | `FastAPI`, `Starlette` | Alto desempenho e facilidade de uso. |
| **DB ORM** | `SQLAlchemy 2.0` | ORM robusto e com suporte assíncrono. |
| **DB Driver** | `asyncpg` | Driver assíncrono para PostgreSQL. |
| **Migrações** | `Alembic` | Gerenciamento de schema do banco de dados. |
| **Recursos** | `fastapi-pagination` | Paginação automática em endpoints GET. |
| **Ambiente** | `Docker`, `python-dotenv` | Contêineres e variáveis de ambiente. |

### Estrutura Modular 🧱

O projeto utiliza uma arquitetura modular, onde cada entidade (atleta, categoria, CT) possui seus próprios:

* **`models.py`**: Definições das tabelas do SQLAlchemy.
* **`schemas.py`**: Modelos de entrada/saída (Pydantic) para validação de dados.
* **`controller.py`**: Lógica de *endpoints* (rotas) e interação com o DB.

---

## ⚠️ Solução de Problemas Comuns

| Erro Comum | Causa no Projeto | Solução Rápida |
| :--- | :--- | :--- |
| `422 Unprocessable Content` | JSON Body malformado ou `Content-Type` ausente no cliente (ex: Postman). | Certifique-se de usar `raw` e selecionar **`JSON`** no Postman e enviar o cabeçalho `Content-Type: application/json`. |
| `500 null value violates not-null constraint` | Erro durante o `db_session.commit()`: um campo obrigatório (ex: `categoria_id`) não foi preenchido. | O objeto `categoria` ou `centro_treinamento` provavelmente não foi encontrado ou não tem a propriedade `pk_id` no momento da inserção. Verifique a **existência** prévia dos dados no DB. |
| `Lentidão em GET /atletas` | **Bug Estrutural:** A rota está executando consultas desnecessárias ao DB (Problema N+1 ou consultas sequenciais). | Refatore a função `query` para **construir a query dinamicamente** e usar `paginate` no DB, executando a consulta apenas uma vez. |

---

## ✨ Contribuição

Sinta-se à vontade para contribuir!

1.  Faça um **Fork** do projeto.
2.  Crie uma nova *branch* (`git checkout -b feature/sua-feature`).
3.  Faça suas alterações e *commit* (`git commit -m 'feat: Adiciona nova funcionalidade X'`).
4.  Envie para a *branch* original (`git push origin feature/sua-feature`).
5.  Abra um **Pull Request**.

💖 Obrigado por checar o projeto!
