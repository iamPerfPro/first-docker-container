# Run Your First Docker Container

A tiny beginner-friendly Docker project from **Bridge With Code**.

The goal is simple:

1. Create a small Python web application
2. Build a Docker image
3. Run a container
4. Open the application in your browser

No advanced Docker knowledge is required.

---

## What You'll Build

A tiny Flask web application that displays:

```text
Hello from Docker!
```

in your browser.

---

## Project Structure

```text
first-docker-container/
│
├── app.py
├── requirements.txt
├── Dockerfile
├── .dockerignore
└── README.md
```

---

# Before You Start

You need:

- Docker installed
- A terminal / command prompt
- A web browser

You do **not** need Python installed on your computer to run the Docker version of this project.

Docker provides the Python environment inside the container.

---

# Step 1 — Clone the Repository

```bash
git clone https://github.com/iamPerfPro/first-docker-container.git
```

Move into the project directory:

```bash
cd first-docker-container
```

---

# Step 2 — Build the Docker Image

Run:

```bash
docker build -t hello-docker .
```

What this means:

- `docker build` builds a Docker image.
- `-t hello-docker` gives the image the name `hello-docker`.
- `.` means use the Dockerfile in the current directory.

---

# Step 3 — Run the Container

Run:

```bash
docker run -p 5000:5000 hello-docker
```

You should see output similar to:

```text
Running on http://0.0.0.0:5000
```

---

# Step 4 — Open the App

Open your browser and visit:

```text
http://localhost:5000
```

You should see:

```text
Hello from Docker!
```

Congratulations — your first Docker container is running.

---

# What Does `-p 5000:5000` Mean?

The command:

```bash
docker run -p 5000:5000 hello-docker
```

maps a port on your computer to a port inside the Docker container.

```text
YOUR COMPUTER        CONTAINER

Port 5000   ----->   Port 5000
```

Flask is running on port `5000` inside the container.

Docker allows your browser to reach it through port `5000` on your computer.

---

# Understanding the Dockerfile

Our Dockerfile:

```dockerfile
FROM python:3.12-slim

WORKDIR /app

COPY requirements.txt .

RUN pip install --no-cache-dir -r requirements.txt

COPY . .

EXPOSE 5000

CMD ["python", "app.py"]
```

## FROM

```dockerfile
FROM python:3.12-slim
```

Start with a lightweight image that already contains Python 3.12.

## WORKDIR

```dockerfile
WORKDIR /app
```

Create and use `/app` as the working directory inside the container.

## COPY requirements.txt

```dockerfile
COPY requirements.txt .
```

Copy the dependency file into the container.

## RUN

```dockerfile
RUN pip install --no-cache-dir -r requirements.txt
```

Install Flask and the application's dependencies.

## COPY

```dockerfile
COPY . .
```

Copy the application source code into the container.

## EXPOSE

```dockerfile
EXPOSE 5000
```

Document that the application uses port 5000.

## CMD

```dockerfile
CMD ["python", "app.py"]
```

Run `python app.py` when the container starts.

---

# macOS Instructions

Install Docker Desktop for Mac.

After Docker Desktop is running, open Terminal.

Check Docker:

```bash
docker --version
```

Then run:

```bash
git clone https://github.com/iamPerfPro/first-docker-container.git
cd first-docker-container

docker build -t hello-docker .
docker run -p 5000:5000 hello-docker
```

Open:

```text
http://localhost:5000
```

---

# Windows Instructions

Install Docker Desktop for Windows.

Docker Desktop commonly uses WSL 2.

After installation, make sure Docker Desktop is running.

Open one of:

- PowerShell
- Windows Terminal
- Command Prompt

Check Docker:

```powershell
docker --version
```

Clone the repository:

```powershell
git clone https://github.com/iamPerfPro/first-docker-container.git
```

Enter the directory:

```powershell
cd first-docker-container
```

Build:

```powershell
docker build -t hello-docker .
```

Run:

```powershell
docker run -p 5000:5000 hello-docker
```

Open:

```text
http://localhost:5000
```

---

# Ubuntu Instructions

If Docker is already installed, check:

```bash
docker --version
```

Clone the repository:

```bash
git clone https://github.com/iamPerfPro/first-docker-container.git
cd first-docker-container
```

Build the image:

```bash
docker build -t hello-docker .
```

Run:

```bash
docker run -p 5000:5000 hello-docker
```

If your Docker installation requires elevated permissions, use:

```bash
sudo docker build -t hello-docker .
sudo docker run -p 5000:5000 hello-docker
```

Then open:

```text
http://localhost:5000
```

---

# Stop the Container

While the container is running in the terminal, press:

```text
CTRL + C
```

---

# Run the Container in the Background

```bash
docker run -d -p 5000:5000 --name hello-docker-container hello-docker
```

See running containers:

```bash
docker ps
```

Stop it:

```bash
docker stop hello-docker-container
```

Remove it:

```bash
docker rm hello-docker-container
```

---

# See Your Docker Images

```bash
docker images
```

You should see an image named:

```text
hello-docker
```

---

# Common Problems

## Docker command not found

If you see:

```text
docker: command not found
```

Docker is either:

- not installed
- not running
- not available in your PATH

Install/start Docker and try again.

## Docker daemon is not running

On macOS or Windows, open **Docker Desktop** and wait until Docker finishes starting.

Then retry:

```bash
docker build -t hello-docker .
```

## Port 5000 is already in use

If another application is already using port 5000, run:

```bash
docker run -p 8080:5000 hello-docker
```

Then visit:

```text
http://localhost:8080
```

The mapping is now:

```text
Computer port 8080
        ↓
Container port 5000
```

---

# Build Again After Changing the Code

After changing `app.py`, rebuild the image:

```bash
docker build -t hello-docker .
```

Then run it again:

```bash
docker run -p 5000:5000 hello-docker
```

---

# Docker Image vs Container

A simple way to think about it:

```text
Dockerfile
    ↓
docker build
    ↓
IMAGE
    ↓
docker run
    ↓
CONTAINER
```

The **image** is the packaged application.

The **container** is a running instance of that image.

---

# Full Process

```bash
git clone https://github.com/iamPerfPro/first-docker-container.git
cd first-docker-container
docker build -t hello-docker .
docker run -p 5000:5000 hello-docker
```

Then open:

```text
http://localhost:5000
```

---

# Bridge With Code

This repository accompanies the Bridge With Code beginner Docker video.

The goal of Bridge With Code is to make computer science and software-development concepts easier to understand through small practical examples.

---

## Next Topics

- Docker Image vs Container
- What does `docker build` actually do?
- Docker port mapping
- Docker volumes
- Docker Compose
- Running multiple containers

---

## Disclaimer

This project is intentionally minimal and is designed for education.

It is not intended to be a production-ready Flask deployment.
