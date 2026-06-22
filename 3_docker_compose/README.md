# Docker Compose

Using Docker Compose to define and run multi-container applications.

---

## 7-02: Install Docker Compose

On Linux, install Docker Compose manually:

```bash
sudo apt install -y python3 python3-pip
sudo pip3 install docker-compose
```

> On Windows and Mac, Docker Compose is included with Docker Desktop.

---

## 7-03: Run a Compose Definition File

### STEP 2 — Start the containers

> Replace `username` with your PC's login username.

**Windows:**
```bash
docker-compose -f C:\Users\username\Documents\com_folder\docker-compose.yml up -d
```

**Mac:**
```bash
docker-compose -f /Users/username/Documents/com_folder/docker-compose.yml up -d
```

**Linux:**
```bash
docker-compose -f /home/username/com_folder/docker-compose.yml up -d
```

### STEP 4 — Stop and remove containers and networks

**Windows:**
```bash
docker-compose -f C:\Users\username\Documents\com_folder\docker-compose.yml down
```

**Mac:**
```bash
docker-compose -f /Users/username/Documents/com_folder/docker-compose.yml down
```

**Linux:**
```bash
docker-compose -f /home/username/com_folder/docker-compose.yml down
```

---

## Included Compose Files

| Directory | Services | Notes |
|---|---|---|
| [`chapter07-03`](chapter07-03/) | WordPress + MySQL (latest) | Basic setup |
| [`chapter07-03column_MySQL8`](chapter07-03column_MySQL8/) | WordPress + MySQL 8 | With UTF-8 and native auth plugin |
| [`chapter07-03column_Redmine`](chapter07-03column_Redmine/) | Redmine + MySQL 5.7 | — |
| [`chapter07-03column_Redmine+MySQL8`](chapter07-03column_Redmine+MySQL8/) | Redmine + MySQL 8 | With UTF-8 and native auth plugin |
| [`chapter07-03column_WordPress+MariaDB`](chapter07-03column_WordPress+MariaDB/) | WordPress + MariaDB | MariaDB alternative |
