# DVWA + Ngrok Setup on Play With Docker

This guide helps you deploy **Damn Vulnerable Web Application (DVWA)** using **Play With Docker (PWD)** and expose it publicly using **Ngrok**.

## ✅ Requirements

Before starting, ensure you have the following:

- 🐳 [Play With Docker Account](https://labs.play-with-docker.com/)
- 🌐 [Ngrok Account](https://dashboard.ngrok.com/endpoints)  
  After registering, get your **Ngrok Authtoken** from the [auth token page](https://dashboard.ngrok.com/get-started/setup).

---

## 📦 Docker Images Used

You can explore the Docker images used in this setup:

- DVWA Official Image:  
  https://hub.docker.com/r/vulnerables/web-dvwa
- Custom DVWA Image with Fixes:  
  https://hub.docker.com/r/kaakaww/dvwa-docker
- Ngrok Image:  
  https://hub.docker.com/r/ngrok/ngrok

---

## 🚀 Step-by-Step Deployment

### 1. Clone or Create `docker-compose.yml`

Create a file named `docker-compose.yml` with the following content:

```yaml
version: "3.8"

services:
  dvwa:
    image: kaakaww/dvwa-docker:latest
    container_name: dvwa
    ports:
      - "80:80"
    restart: unless-stopped
