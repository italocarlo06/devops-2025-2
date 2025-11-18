## 🐳 Running with Docker Compose

This project includes a `docker-compose.yml` file to orchestrate the application (NestJS API) and the database (PostgreSQL) simultaneously.

### 1\. Environment Configuration

The Docker setup relies on environment variables defined in the `docker-compose.yml`. Before running the containers, you must create a `.env` file in the root directory.

**Create a `.env` file with the following content:**

```dotenv
# API Image Version
DOCKER_IMAGE_TAG=latest

# Database Credentials & Configuration
DB_USER=postgres
DB_PASSWORD=postgres
DB_NAME=aula_devops_db

# Internal Database Port (Keep this as 5432 for internal container communication)
DB_PORT=5432
```

> **Note:** The `DATABASE_URL` is automatically constructed inside the Docker composition using these variables. You do not need to manually set the connection string for the Docker environment.

### 2\. Starting the Services

To download the images and start the containers in detached mode (background), run:

```bash
docker compose up -d
```

**What happens next?**

1.  The **PostgreSQL** container starts.
2.  The **API** container waits for the database to be "healthy" (via a health check).
3.  Once the database is ready, the API starts and connects automatically.

### 3\. Accessing the Application

| Service | Local Address | Host Port | Internal Port |
| :--- | :--- | :--- | :--- |
| **API (NestJS)** | `http://localhost:3000` | `3000` | `3000` |
| **PostgreSQL** | `localhost` | `35432` | `5432` |

> ⚠️ **Database Connection:** If you want to connect to the database using an external tool (like DBeaver, PgAdmin, or TablePlus), please use port **35432**. The standard port `5432` is reserved for internal communication between the API and the DB container.

### 4\. Useful Commands

  * **View real-time logs:**

    ```bash
    docker compose logs -f
    ```

  * **Stop all containers:**

    ```bash
    docker compose down
    ```

  * **Force rebuild (if you updated the image tag):**

    ```bash
    docker compose up -d --force-recreate
    ```

-----

**Would you like me to create a diagram of the architecture (API \<-\> Network \<-\> DB) to add to this section as well?**
