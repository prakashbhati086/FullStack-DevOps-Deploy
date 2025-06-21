Project Overview
FullStack DevOps Deployment is a personal project built to demonstrate my hands-on DevOps skills using a simple Node.js application. The application includes a basic homepage, login, and signup functionality, connected to a MongoDB database.

The main focus of this project is not the application itself, but the DevOps workflow built around it — from development to automated deployment using modern tools.

🎯 Purpose of the Project
This project was created to:

Practice and demonstrate a complete DevOps pipeline

Automate build, test, and deployment processes

Learn how to manage applications using Docker and Kubernetes

Implement continuous integration and continuous deployment (CI/CD) with Jenkins

It reflects real-world DevOps practices, including containerization, orchestration, automation, and microservice deployment.

🛠️ Tools and Technologies Used
Category	Tools
Version Control	Git, GitHub
CI/CD Pipeline	Jenkins
Containers	Docker
Orchestration	Kubernetes (Minikube)
Backend Database	MongoDB (Docker image)
Application	Node.js (Express), HTML/CSS


My Approach & DevOps Workflow
This project was a complete learning experience in implementing DevOps principles from scratch. Below is how I approached it and the tools I used throughout the pipeline:

🧾 1. Version Control with Git & GitHub
I started by writing a basic Node.js application with HTML/CSS for UI and MongoDB as the database. I used Git for version control and hosted the project repository on GitHub. This made it easy to collaborate, track changes, and integrate with Jenkins for automation.

🔁 2. CI/CD Pipeline using Jenkins
I set up Jenkins on my local machine and created a multistage pipeline to:

Clone the project from GitHub

Install dependencies using npm install

Generate a unique Docker image tag using Git commit hash + Jenkins build number

Build and push the Docker image to Docker Hub

Problem I faced:
Windows Jenkins doesn’t support shell scripts well (sh), so I had to use bat commands in Jenkinsfile.
How I solved it:
I rewrote all shell commands in bat syntax for Windows compatibility.

🐳 3. Containerization with Docker
I created a Dockerfile to containerize my Node.js app. The image was tagged dynamically with every build to keep track of each deployment version.

Problem I faced:
Initial builds failed due to missing dependencies and path issues in the container.
Solution:
I fixed it by defining the correct working directory in the Dockerfile and using multi-stage tagging carefully in Jenkins.

☸️ 4. Orchestration with Kubernetes
I used Minikube to simulate a Kubernetes cluster locally. I created separate YAML files for:

Deploying MongoDB using the official mongo:latest image

Deploying the Node.js app using the pushed Docker image

Persistent volume setup for MongoDB

Services for internal/external access

Problem I faced:
Kubernetes kubectl apply failed in Jenkins due to missing permissions and kubeconfig.
How I solved it:
I manually copied my Minikube config and certificates to Jenkins's home directory (/var/lib/jenkins) and granted the correct file permissions.

🧪 5. Automated Deployment
Finally, I updated my Jenkins pipeline to automatically:

Replace the image tag inside nodeapp-deployment.yml

Apply all Kubernetes YAML files using kubectl

This completed the full CI/CD loop — every code push now triggers an image build, a Docker push, and a fresh deployment to Kubernetes.

✅ What I Learned
Building CI/CD pipelines with real-world DevOps tools

Handling platform-specific scripting issues (Windows bat vs Linux sh)

Docker image tagging and version management

Managing Kubernetes configs, permissions, and deployment structure

Debugging YAMLs, Dockerfile, and Jenkins integration

Essential DevOps Commands Used (and Must-Know)
🟦 Git & GitHub (Version Control)
Command	Purpose
git init	Initialize a Git repo locally
git clone <repo-url>	Clone a GitHub repo
git add .	Stage all files for commit
git commit -m "message"	Commit staged changes
git push origin main	Push local commits to GitHub
git pull	Fetch and merge changes from remote
git status	Show file changes and staging status
git rev-parse --short HEAD ✅	Get short Git commit hash (used for Docker tag)

🧪 NPM & Node.js (App Layer)
Command	Purpose
npm install ✅	Install Node.js project dependencies
npm start	Start the Node.js application
npm run <script>	Run custom scripts from package.json

🐳 Docker (Containerization)
Command	Purpose
docker build -t <name:tag> . ✅	Build a Docker image
docker tag <src> <target> ✅	Tag an existing image with another name
docker push <name:tag> ✅	Push image to Docker Hub
docker images	List all local images
docker ps	List running containers
docker run -d -p 3000:3000 <image>	Run a container in detached mode
docker login ✅	Login to Docker Hub
docker-compose up	Start services defined in docker-compose.yml
docker rm <container> / docker rmi <image>	Remove container/image

🔁 Jenkins (CI/CD)
Command/Snippet	Purpose
pipeline { ... } ✅	Define Jenkins declarative pipeline
bat 'npm install' ✅	Run Windows commands in Jenkins
bat 'docker build ...' ✅	Run Docker build in Jenkins
withCredentials([usernamePassword(...)]) ✅	Use Docker credentials securely
env.IMAGE_TAG = ... ✅	Dynamically generate image tag using Git hash
git branch: ..., url: ... ✅	Clone Git repo inside Jenkinsfile

☸️ Kubernetes (Orchestration)
Command	Purpose
kubectl apply -f <file> ✅	Deploy/update resources using YAML
kubectl get pods ✅	List all running pods
kubectl get services ✅	View Kubernetes services and IPs
kubectl delete -f <file>	Delete resources defined in YAML
kubectl logs <pod-name>	View logs for a pod
kubectl describe pod <name>	Inspect pod in detail
kubectl get all	Get all resources in current namespace
minikube start ✅	Start a local Kubernetes cluster
minikube dashboard ✅	Launch GUI dashboard
minikube ip ✅	Get Minikube's IP address

