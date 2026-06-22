# Docker Sample Files

A collection of sample files and commands for learning Docker, covering multi-container setups, advanced container operations, and Docker Compose.

## Repository Structure

```
.
├── 1_multiple_containers/    # Running multiple containers together
│   └── readme.txt
├── 2_advanced_containers/    # File copying, volume mounting, and image creation
│   ├── readme.txt
│   ├── index.html            # Sample HTML file for Apache containers
│   └── Dockerfile/
│       └── Dockerfile        # Sample Dockerfile for building a custom Apache image
└── 3_docker_compose/         # Docker Compose definition files
    ├── readme.txt
    ├── chapter07-03/                           # WordPress + MySQL
    ├── chapter07-03column_MySQL8/              # WordPress + MySQL 8
    ├── chapter07-03column_Redmine/             # Redmine + MySQL 5.7
    ├── chapter07-03column_Redmine+MySQL8/      # Redmine + MySQL 8
    └── chapter07-03column_WordPress+MariaDB/   # WordPress + MariaDB
```

## Contents

### 1. Multiple Containers

Step-by-step commands for creating and connecting multiple containers on a Docker network:

- **WordPress + MySQL** — Create a network, launch MySQL and WordPress containers, and connect them
- **Redmine + MySQL** — Same pattern with Redmine and MySQL
- **Redmine + MariaDB** — Redmine with MariaDB as the database
- **WordPress + MariaDB** — WordPress with MariaDB as the database

### 2. Advanced Containers

Covers more advanced Docker operations:

- **File copying** (`docker cp`) — Copy files between host and container
- **Bind mount** — Mount a host directory into a container
- **Volume mount** — Create and mount a Docker volume
- **Volume backup/restore** — Back up and restore volume data using a busybox container
- **Image creation** — Create images from containers using `docker commit` and `docker build`

### 3. Docker Compose

Docker Compose definition files (`docker-compose.yml`) for various service combinations:

| Directory | Services |
|---|---|
| `chapter07-03` | WordPress + MySQL (latest) |
| `chapter07-03column_MySQL8` | WordPress + MySQL 8 |
| `chapter07-03column_Redmine` | Redmine + MySQL 5.7 |
| `chapter07-03column_Redmine+MySQL8` | Redmine + MySQL 8 |
| `chapter07-03column_WordPress+MariaDB` | WordPress + MariaDB |

## Prerequisites

- [Docker](https://www.docker.com/) installed and running
- [Docker Compose](https://docs.docker.com/compose/) (included with Docker Desktop on Windows/Mac; install separately on Linux)

## Usage

### Running containers manually

Refer to the `readme.txt` in each directory for step-by-step commands. For example, to set up WordPress with MySQL:

```bash
# Create a network
docker network create wordpress000net1

# Start MySQL
docker run --name mysql000ex11 -dit --net=wordpress000net1 \
  -e MYSQL_ROOT_PASSWORD=myrootpass \
  -e MYSQL_DATABASE=wordpress000db \
  -e MYSQL_USER=wordpress000kun \
  -e MYSQL_PASSWORD=wkunpass \
  mysql --character-set-server=utf8mb4 --collation-server=utf8mb4_unicode_ci

# Start WordPress
docker run --name wordpress000ex12 -dit --net=wordpress000net1 -p 8085:80 \
  -e WORDPRESS_DB_HOST=mysql000ex11 \
  -e WORDPRESS_DB_NAME=wordpress000db \
  -e WORDPRESS_DB_USER=wordpress000kun \
  -e WORDPRESS_DB_PASSWORD=wkunpass \
  wordpress
```

Then open http://localhost:8085 in your browser.

### Using Docker Compose

```bash
cd 3_docker_compose/chapter07-03
docker-compose up -d
```

To stop and remove:

```bash
docker-compose down
```
