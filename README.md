
# 🐳 Laravel Enterprise Docker Environment

This repository provides a high-performance, containerized development environment specifically tuned for Laravel applications. It features a modular architecture using **PHP 8.2-FPM**, **Nginx (Alpine)**, and **MariaDB 10.11**.

---

## 🧐 What is Docker & Why Use It?

**Docker** is a containerization platform that bundles your application code with the exact server environment it needs to run.

**Key Advantages:**
* **Eliminate "Environment Drift"**: Guarantees that the app runs exactly the same in development as it does on a production server.
* **Modular Isolation**: Run MariaDB and PHP in separate containers that only talk to each other over a secure virtual network.
* **Instant Deployment**: Use one command to build and launch your entire infrastructure.



---

## 🛠️ Quick Start & Setup

### 1. Prerequisites
Ensure you have the following installed:
* **Docker Desktop** (or Docker Engine on Linux)
* **Docker Compose V2**

### 2. Installation Steps
1. **Copy Files**: Place `docker-compose.yml`, `Dockerfile`, and the `docker/` folder into your Laravel root directory.
2. **Configure `.env`**: Update your Laravel environment variables to route traffic correctly:
   * `DB_HOST=db` (The service name defined in `docker-compose.yml`)
   * `DB_PORT=3306` (Internal container port)
   * `DB_DATABASE=sugarmill_db`
   * `DB_USERNAME=sugarmill_user`
   * `DB_PASSWORD=sugarmill_password`
3. **Launch**:
   ```bash
   docker compose up -d --build


## 🌐 Service Discovery & Access

Once active, the environment maps internal container services to your local machine (Host).

| Service | Host URL / Endpoint | Internal Container Port |
| --- | --- | --- |
| **Laravel App** | [http://localhost:8081](https://www.google.com/search?q=http://localhost:8081) | `80` |
| **phpMyAdmin** | [http://localhost:8082](https://www.google.com/search?q=http://localhost:8082) | `80` |
| **MariaDB** | `127.0.0.1:3307` | `3306` |

---

## ⚙️ Advanced Configuration (Port Mapping)

To avoid conflicts with other local projects, you can change the **Host Port** in the `docker-compose.yml` file.

**Syntax**: `- "HOST_PORT:CONTAINER_PORT"`

* **To change the App port**: Change `8081:80` to `9000:80`. Access it at `localhost:9000`.
* **To change the DB port**: Change `3307:3306` to `3308:3306`. Update your external DB client to port `3308`.

---

## 📜 Professional Cheat Sheet & Tools

### Lifecycle Management

| Command | Action |
| --- | --- |
| `docker compose up -d` | Launch services in detached mode. |
| `docker compose down` | Stop and remove containers and networks. |
| `docker compose ps` | View running status and port health. |
| `docker compose logs -f` | Stream real-time PHP/Nginx error logs. |

### Tooling & Commands

Run these inside the container so you don't need PHP installed on your PC:

* **Enter Shell**: `docker exec -it laravel_app bash`
* **Artisan**: `docker exec laravel_app php artisan migrate`
* **Composer**: `docker exec laravel_app composer install`

---

## 🗄️ Database Management (Enterprise Workflows)

For large-scale data (like **Sugar Mill** or **CMRL** systems), avoid browser-based exports which can time out. Use the high-speed CLI utility:

**Full Database Export (Backup):**

```bash
docker exec laravel_mariadb mariadb-dump -u sugarmill_user -p"sugarmill_password" sugarmill_db > backup.sql

```

**Full Database Import (Restore):**

```bash
docker exec -i laravel_mariadb mariadb -u sugarmill_user -p"sugarmill_password" sugarmill_db < backup.sql

```

---

## ❓ Troubleshooting

* **Port Conflict**: If a container fails to start, check if another app is using the port (e.g., `8081`).
* **Permissions**: If you see "Permission Denied" in Laravel, run:
`docker exec laravel_app chown -R www-data:www-data storage bootstrap/cache`
* **Database Connection Refused**: Ensure your `.env` `DB_HOST` is set to `db`, not `localhost`.

---

