# 🐳 Reducing Docker Image Size Using Multi-Stage Build

- Compressing a Python Docker image from **~1 GB** to just **~142 MB** using multi-stage builds.

---

## 🚀 Overview

Docker images can easily become bloated, especially when packaging Python apps with all dependencies. This project demonstrates how to use **multi-stage Docker builds** to dramatically reduce image size without sacrificing functionality.

---

## 📉 Before & After

| Stage        | Base Image          | Size         |
|--------------|---------------------|--------------|
| Stage 1      | `python:3.7`         | ~1.01 GB     |
| Final Output | `python:3.7-slim`    | ~142 MB      |

---

## 🛠️ How It Works

### 🔧 Stage 1: Dependency Installation

```dockerfile
FROM python:3.7 AS builder

WORKDIR /app

COPY requirements.txt .

RUN pip install -r requirements.txt
```
# 🎯 Stage 2: Lightweight Runtime
```
FROM python:3.7-slim

WORKDIR /app

COPY --from=builder /usr/local/lib/python3.7/site-packages/ /usr/local/lib/python3.7/site-packages/

COPY . .

ENTRYPOINT [ "python", "run.py" ]
```
- Copies only the installed dependencies and source code into a lightweight image.
- Final image is significantly smaller and production-ready.

# ✅ Benefits
- 🚀 Faster deployment times
- 🔐 Smaller attack surface
- 💾 Reduced storage & bandwidth usage
- 🔄 Easier CI/CD integration

# 📌 Prerequisites
- Docker installed locally
- requirements.txt and run.py in your project root

# FULL MULTI-STAGE BUILD DOCKERFILE:
```
#stage 1 base image 994 mb ~ 1.05gb
FROM python:3.7 AS builder

WORKDIR /app

COPY requirements.txt .

RUN pip install -r requirements.txt

#--------
# stage 2 base image  400 mb
FROM python:3.7-slim

WORKDIR /app

COPY --from=builder /usr/local/lib/python3.7/site-packages/ /usr/local/lib/python3.7/site-packages/

COPY . .

ENTRYPOINT [ "python", "run.py"]
```

# build it 
```
docker build -t flask-app-mini .
docker images
```

# RESULT :

![image](https://github.com/user-attachments/assets/c686fef8-c802-4472-af7b-4ce418b64088)


