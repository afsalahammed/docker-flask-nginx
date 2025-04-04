# **Dockerized Flask App with Nginx (Reverse Proxy Setup)** 🐳🌐

## **📌 Overview**
This project demonstrates how to containerize a basic **Flask web application** using **Docker** and serve it through **Nginx as a reverse proxy** using **Docker Compose**. This is a beginner-friendly setup to understand how multiple services (app + web server) can work together inside containers.

---

## **🛠️ How It Works**
- The **Flask app** serves a simple web page on port 5000.
- **Nginx** acts as a **reverse proxy**, routing external traffic to the Flask app running in a separate container.
- **Docker Compose** handles multi-container orchestration, making setup and teardown easy.
- A `.dockerignore` file ensures a clean image build by excluding unnecessary files.

---

## **📁 Project Structure**
```
docker-flask-nginx/
├── app/
│   ├── app.py              # Main Flask application
│   └── requirements.txt    # Python dependencies (Flask)
├── nginx/
│   └── default.conf        # Nginx reverse proxy configuration
├── docker-compose.yml      # Defines services: Flask app & Nginx
├── Dockerfile              # Image build steps for Flask app
└── .dockerignore           # Ignore files during Docker image build
```

---

## **🔍 Components Explained**

### ✅ `app/app.py`
- A simple Flask web application.
- Exposes one route returning a success message.
- Runs on `host=0.0.0.0` so it’s accessible from the container network.

### ✅ `app/requirements.txt`
- Lists Python dependencies for the Flask app.
- Typically includes `flask` or any other Python packages.

### ✅ `nginx/default.conf`
- Nginx configuration file.
- Routes incoming traffic (e.g., on port 80) to the Flask container on port 5000.
- Acts as a **reverse proxy**, improving performance and adding an abstraction layer.

### ✅ `Dockerfile`
- Builds a Docker image for the Flask app.
- Sets up the working directory, installs Python packages, and starts the app.
- Built separately from Nginx — this allows flexibility and separation of concerns.

### ✅ `docker-compose.yml`
- Defines two services:
  1. **`web`** – Flask app container built from Dockerfile.
  2. **`nginx`** – Nginx container using a standard image and custom config.
- Handles networking between services using Docker's bridge network.

### ✅ `.dockerignore`
- Excludes unnecessary files/folders from being copied to the Docker image.
- Helps reduce image size and speeds up the build process.

---

## **🚀 How to Run the Project**

1️⃣ **Build & Start All Containers**
```bash
docker-compose up --build
```

2️⃣ **Visit in Browser**
```bash
http://localhost
```
✅ You should see the response served by the Flask app via Nginx.

3️⃣ **Stop the Containers**
```bash
docker-compose down
```

---

## **💡 Why This Setup?**
- **Nginx** improves scalability, security, and performance.
- **Flask** handles backend logic and is isolated in its own container.
- **Docker Compose** makes managing multi-container apps effortless.
- This separation mirrors real-world deployment patterns in cloud-native apps.

---

## **🔐 Security Best Practices**
- Use minimal base images (e.g., `python:3.9-slim`) to reduce vulnerabilities.
- Don't store secrets in images. Use `.env` files or secret managers.
- Keep dependencies up-to-date.
- Avoid exposing unnecessary ports.

---

## **📦 Next Steps**
- Add HTTPS support using **Let’s Encrypt** or a self-signed certificate.
- Deploy on **AWS ECS**, **GCP**, or **Azure**.
- Integrate a **database** service via Docker Compose.
- Add **logging**, **monitoring**, or **CI/CD** with GitHub Actions.

---

## **🤝 Contributing**
You’re welcome to fork, clone, modify, or scale this project. This structure serves as a great foundation for building full-stack or microservice applications in containerized environments.
