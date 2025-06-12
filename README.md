# DVWA + Ngrok Setup on Play With Docker

This guide helps you deploy **Damn Vulnerable Web Application (DVWA)** using **Play With Docker (PWD)** and expose it publicly using **Ngrok**.

## ✅ Requirements

Before starting, ensure you have the following:

- 🐳 [Play With Docker Account](https://labs.play-with-docker.com/)
- 🌐 [Ngrok Account](https://dashboard.ngrok.com/endpoints)  
- After registering, get your **Ngrok Authtoken** from the [auth token page](https://dashboard.ngrok.com/get-started/setup).

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

## 🚀 Step-by-Step Deployment (Options 1)

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
```
### 2. Start DVWA using Docker Compose
```
docker-compose up -d
```
### 3. Pull Ngrok Docker Image
```
docker pull ngrok/ngrok
```
### 4. Run Ngrok to Expose Port 80
```
docker run --net=host -it -e NGROK_AUTHTOKEN={YOUR_NGROK_TOKEN} --name ngrok ngrok/ngrok:latest http 80
```
### 5. Get The URL Link DVWA Webapps
You Will see the URL
```
Session Status                online                                                                  
Account                       xxx@gmail.com (Plan: Free)                                        
Version                       3.23.1                                                                  
Region                        Asia Pacific (ap)                                                       
Latency                       30ms                                                                    
Web Interface                 http://0.0.0.0:4040                                                     
Forwarding                    https://xxxx-xxx-xx-xxx-xxx.ngrok-free.app -> http://localhost:80       
                                                                                                      
Connections                   ttl     opn     rt1     rt5     p50     p90                             
                              2       0       0.00    0.00    5.13    5.20                            
                                                                                                      
HTTP Requests                                                                                         
-------------
```
---

## 🚀 Step-by-Step Deployment (Options 2)

### 1. Clone or Create `docker-compose.yml`

Create a file named `docker-compose.yml` with the following content:

```yaml
version: '3.8'

services:
  dvwa:
    image: kaakaww/dvwa-docker:latest
    container_name: dvwa
    ports:
      - "80:80"
    restart: unless-stopped

  ngrok:
    image: ngrok/ngrok:latest
    container_name: ngrok
    restart: unless-stopped
    depends_on:
      - dvwa
    environment:
      NGROK_AUTHTOKEN: {YOUR_NGROK_TOKEN}
    command: http dvwa:80

```
### 2. Start DVWA using Docker Compose
```
docker-compose up -d
```
### 3. Get The URL Link DVWA Webapps on the Ngrok
Visit the Ngrok Dashboard >> Open the Menu "Endpoints" click the Url
```
https://dashboard.ngrok.com/endpoints
```
