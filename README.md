

---

# 🐳 Laravel & MariaDB Docker Environment

This repository provides a production-ready, containerized development environment for Laravel applications. It uses **PHP 8.2-FPM**, **Nginx**, and **MariaDB 10.11**.

## 🧐 What is Docker & Why Use It?

**Docker** is a platform that allows you to package an application and all its dependencies (PHP, extensions, libraries, database) into a single "container".

**Why use it?**

* **Environment Consistency**: It solves the "it works on my machine" problem. Your Laravel project will run exactly the same in Delhi, on a colleague's machine, or on a production server.
* **Isolation**: You can run different projects with different versions (e.g., PHP 7.4 vs PHP 8.2) on the same computer without conflicts.
* **Speed**: You can set up a complex stack (Database, Cache, Web Server) in seconds using a single command.

---

## 🛠️ Quick Start

1. **Extract files**: Place `docker-compose.yml`, `Dockerfile`, and the `docker/` folder in your Laravel root.
2. **Configure `.env**`: Update your Laravel environment variables:
* `DB_HOST=db`
* `DB_PORT=3306`
* `DB_DATABASE=sugarmill_db`
* `DB_USERNAME=sugarmill_user`
* `DB_PASSWORD=sugarmill_password`


3. **Launch**:
```bash
docker compose up -d --build

```



---

## 📜 Professional Docker Cheat Sheet

### Essential Lifecycle Commands

| Command | Purpose |
| --- | --- |
| `docker compose up -d` | Start all services in the background. |
| `docker compose down` | Stop and remove all containers. |
| `docker compose ps` | List all running containers and their status. |
| `docker compose logs -f` | Follow real-time logs (great for debugging PHP errors). |
| `docker compose build` | Re-read the Dockerfile and rebuild the images. |

### Container Interaction

| Command | Purpose |
| --- | --- |
| `docker exec -it laravel_app bash` | Open a terminal inside your PHP container. |
| `docker exec laravel_app php artisan migrate` | Run Laravel migrations from the host. |
| `docker exec laravel_app composer install` | Install PHP dependencies inside the container. |

---

## 🗄️ Reliable Database Backups (CLI)

Never rely on web-based exports (like phpMyAdmin) for large projects like **Sugar Mill** or **CMRL** systems, as they often time out. Use these professional CLI commands for 100% data integrity.

**Export (Backup):**

```bash
docker exec laravel_mariadb mariadb-dump -u sugarmill_user -p"sugarmill_password" sugarmill_db > full_backup.sql

```

**Import (Restore):**

```bash
docker exec -i laravel_mariadb mariadb -u sugarmill_user -p"sugarmill_password" sugarmill_db < full_backup.sql

```

---

