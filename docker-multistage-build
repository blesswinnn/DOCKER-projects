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
