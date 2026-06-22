# Multiple Containers

Step-by-step commands for creating and connecting multiple containers on a Docker network.

---

## 5-02: WordPress + MySQL

### STEP 1 — Create a network

```bash
docker network create wordpress000net1
```

### STEP 2 — Create and start a MySQL container

```bash
docker run --name mysql000ex11 -dit --net=wordpress000net1 \
  -e MYSQL_ROOT_PASSWORD=myrootpass \
  -e MYSQL_DATABASE=wordpress000db \
  -e MYSQL_USER=wordpress000kun \
  -e MYSQL_PASSWORD=wkunpass \
  mysql --character-set-server=utf8mb4 --collation-server=utf8mb4_unicode_ci
```

### STEP 3 — Create and start a WordPress container

```bash
docker run --name wordpress000ex12 -dit --net=wordpress000net1 -p 8085:80 \
  -e WORDPRESS_DB_HOST=mysql000ex11 \
  -e WORDPRESS_DB_NAME=wordpress000db \
  -e WORDPRESS_DB_USER=wordpress000kun \
  -e WORDPRESS_DB_PASSWORD=wkunpass \
  wordpress
```

### STEP 4 — Verify that the containers are running

```bash
docker ps
```

### STEP 6 — Clean up

```bash
docker stop wordpress000ex12
docker stop mysql000ex11
docker rm wordpress000ex12
docker rm mysql000ex11
docker network rm wordpress000net1
```

---

## 5-03: Exercises

**Answer 1** — Refer to [STEP 3](#step-3--create-and-start-a-wordpress-container) above.

**Answer 2** — Refer to [STEP 3](#step-3--create-and-start-a-wordpress-container) above.

---

## 5-04: Redmine and MySQL

### Create a network

```bash
docker network create redmine000net2
```

### Create and start a MySQL container

```bash
docker run --name mysql000ex13 -dit --net=redmine000net2 \
  -e MYSQL_ROOT_PASSWORD=myrootpass \
  -e MYSQL_DATABASE=redmine000db \
  -e MYSQL_USER=redmine000kun \
  -e MYSQL_PASSWORD=rkunpass \
  mysql --character-set-server=utf8mb4 --collation-server=utf8mb4_unicode_ci
```

### Create and start a Redmine container

```bash
docker run -dit --name redmine000ex14 --network redmine000net2 -p 8086:3000 \
  -e REDMINE_DB_MYSQL=mysql000ex13 \
  -e REDMINE_DB_DATABASE=redmine000db \
  -e REDMINE_DB_USERNAME=redmine000kun \
  -e REDMINE_DB_PASSWORD=rkunpass \
  redmine
```

---

## 5-04: Redmine and MariaDB

### Create a network

```bash
docker network create redmine000net3
```

### Create and start a MariaDB container

```bash
docker run --name mariadb000ex15 -dit --net=redmine000net3 \
  -e MYSQL_ROOT_PASSWORD=mariarootpass \
  -e MYSQL_DATABASE=redmine000db \
  -e MYSQL_USER=redmine000kun \
  -e MYSQL_PASSWORD=rkunpass \
  mariadb --character-set-server=utf8mb4 --collation-server=utf8mb4_unicode_ci
```

### Create and start a Redmine container

```bash
docker run -dit --name redmine000ex16 --network redmine000net3 -p 8087:3000 \
  -e REDMINE_DB_MYSQL=mariadb000ex15 \
  -e REDMINE_DB_DATABASE=redmine000db \
  -e REDMINE_DB_USERNAME=redmine000kun \
  -e REDMINE_DB_PASSWORD=rkunpass \
  redmine
```

---

## 5-04: WordPress and MariaDB

### Create a network

```bash
docker network create wordpress000net4
```

### Create and start a MariaDB container

```bash
docker run --name mariadb000ex17 -dit --net=wordpress000net4 \
  -e MYSQL_ROOT_PASSWORD=mariarootpass \
  -e MYSQL_DATABASE=wordpress000db \
  -e MYSQL_USER=wordpress000kun \
  -e MYSQL_PASSWORD=wkunpass \
  mariadb --character-set-server=utf8mb4 --collation-server=utf8mb4_unicode_ci
```

### Create and start a WordPress container

```bash
docker run --name wordpress000ex18 -dit --net=wordpress000net4 -p 8088:80 \
  -e WORDPRESS_DB_HOST=mariadb000ex17 \
  -e WORDPRESS_DB_NAME=wordpress000db \
  -e WORDPRESS_DB_USER=wordpress000kun \
  -e WORDPRESS_DB_PASSWORD=wkunpass \
  wordpress
```
