# Advanced Containers

Covers file copying, volume mounting, image creation, and Dockerfiles.

---

## 6-02: Copying Files

### STEP 0 — Create an Apache container

```bash
docker run --name apa000ex19 -d -p 8089:80 httpd
```

### Preparation — Create the index.html file

Refer to the [`index.html`](index.html) in this folder.

### STEP 1 — Copy a file from the container to the host

> Replace `username` with your PC's login username.

**Windows:**
```bash
docker cp apa000ex19:/usr/local/apache2/htdocs/index.html C:\Users\username\Documents\
```

**Mac:**
```bash
docker cp apa000ex19:/usr/local/apache2/htdocs/index.html /Users/username/Documents/
```

**Linux:**
```bash
docker cp apa000ex19:/usr/local/apache2/htdocs/index.html /home/username/
```

### STEP 2 — Copy a file from the host to the container

> Replace `username` with your PC's login username.

**Windows:**
```bash
docker cp C:\Users\username\Documents\index.html apa000ex19:/usr/local/apache2/htdocs/
```

**Mac:**
```bash
docker cp /Users/username/Documents/index.html apa000ex19:/usr/local/apache2/htdocs/
```

**Linux:**
```bash
docker cp /home/username/index.html apa000ex19:/usr/local/apache2/htdocs/
```

---

## 6-03: Mounting Storage Volumes

### Bind Mount — Start an Apache container with a bind mount

> Replace `username` with your PC's login username.

**Windows:**
```bash
docker run --name apa000ex20 -d -p 8090:80 \
  -v C:\Users\username\Documents\apa_folder:/usr/local/apache2/htdocs httpd
```

**Mac:**
```bash
docker run --name apa000ex20 -d -p 8090:80 \
  -v /Users/username/Documents/apa_folder:/usr/local/apache2/htdocs httpd
```

**Linux:**
```bash
docker run --name apa000ex20 -d -p 8090:80 \
  -v /home/username/apa_folder:/usr/local/apache2/htdocs httpd
```

### Advanced: Volume Mount

#### STEP 1 — Create a volume

```bash
docker volume create apa000vol1
```

#### STEP 2 — Start an Apache container with the volume

```bash
docker run --name apa000ex21 -d -p 8091:80 \
  -v apa000vol1:/usr/local/apache2/htdocs httpd
```

#### STEP 3 — Display volume details

```bash
# Inspect the volume
docker volume inspect apa000vol1

# Inspect the container
docker container inspect apa000ex21
```

#### STEP 4 — Clean up

```bash
docker volume rm apa000vol1
```

### Column: Volume Backup

**Backup:**
```bash
docker run --rm \
  -v apa000vol1:/source \
  -v C:\Users\username\Documents:/dest \
  busybox tar czvf /dest/backup_apa.tar.gz -C /source .
```

**Restore:**
```bash
docker run --rm \
  -v apa000vol2:/source \
  -v C:\Users\username\Documents:/dest \
  busybox tar xzvf /dest/backup_apa.tar.gz -C /source
```

---

## 6-04: Creating Images

### STEP 0 — Create an Apache container

```bash
docker run --name apa000ex22 -d -p 8092:80 httpd
```

### STEP 1 — Export a container as an image

```bash
docker commit apa000ex22 ex22_original1
```

### STEP 2 — Verify the image was created

```bash
docker image ls
```

### Advanced: Create an Image Using a Dockerfile

#### STEP 2 — Create a Dockerfile

Refer to the [`Dockerfile`](Dockerfile/Dockerfile) in this folder.

#### STEP 3 — Build the image

> Replace `username` with your PC's login username.

**Windows:**
```bash
docker build -t ex22_original2 C:\Users\username\Documents\apa_folder\
```

**Mac:**
```bash
docker build -t ex22_original2 /Users/username/Documents/apa_folder/
```

**Linux:**
```bash
docker build -t ex22_original2 /home/username/apa_folder/
```

#### STEP 4 — Verify the image was created

```bash
docker image ls
```
