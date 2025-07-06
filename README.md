


# 🏦 End-to-End Bank Application (Spring Boot + MySQL) Deployment using Docker on AWS


This project is a multi-tier **Banking Application** developed using **Java (Spring Boot)** and **MySQL**, containerized with **Docker**, and deployed on **AWS** infrastructure.

---

## 📊 Architecture Diagram
![Screenshot 2025-07-06 140309](https://github.com/user-attachments/assets/87030e22-a4b3-458a-8725-9f755a48c7f0)




---
This is login page
![Screenshot 2025-07-06 140350](https://github.com/user-attachments/assets/b6e00ab6-4c73-434e-9986-8c40e918243b)
## 🛠️ Tech Stack

- **Java** (Spring Boot)
- **MySQL** (Relational Database)
- **Docker** (Containerization)
- **Docker Compose** (Multi-container setup)
- **Maven** (Build Tool)
- **AWS EC2** (VM deployment)
- **AWS ECR** (Docker image hosting)
- **GitHub** (Version Control)

---

## 📦 Folder Structure

```
springboot-bankapp/
│
├── src/                      # Application source code
├── Dockerfile                # Docker build file
├── docker-compose.yml        # Compose file for app + DB
├── images/                   # Architecture & flow images
├── README.md                 # Project Documentation
└── Dockerfile               # Docker build file
```

---

## 🚀 Steps to Deploy on AWS

## ✅ Pre-requisites

- **AWS Account**
- **EC2 Instance** with the following configuration:
  - Instance Type: `t2.medium` (2 vCPUs, 4 GB RAM)
  - AMI: Ubuntu 22.04 LTS (Recommended)
  - Storage: At least 10 GB (SSD)
  - Open the following ports in **Security Group**:
    - `22` (SSH)
    - `8080` (App)
    - `3306` (MySQL)

- **Installed on EC2:**
  - Docker
  - Docker Compose
  - Java 17 or above (if not containerized)
  - Git
  - Maven (for building locally if needed)




### 🧱 Build and Run

### Step 1. **Clone this repository**
   ```bash
   git clone https://github.com/ajay-mall13/springboot-bankapp.git
   cd springboot-bankapp
   ```

### Step 2. **Build the project JAR**
   ```bash
   ./mvnw clean package
   ```

### Step 3. **Build Docker image**
   ```bash
   docker build -t bankapp-mini:latest .
   ```

### Step 4: Create Docker Bridge Network

```bash
docker network create -d bridge bankapp
```



### Step 5: Run MySQL Container

```bash
docker run -itd --name mysql   -e MYSQL_ROOT_PASSWORD=Test@123   -e MYSQL_DATABASE=BankDB   --network=bankapp   mysql
```


### Step 6: Run Spring Boot Application
this  command to start a Spring Boot app container connected to a MySQL database 
```bash
docker run -itd   --name BankApp   -e SPRING_DATASOURCE_USERNAME="root"   -e SPRING_DATASOURCE_PASSWORD="test@123"   -e SPRING_DATASOURCE_URL="jdbc:mysql://mysql:3306/BankDB?useSSL=false&allowPublicKeyRetrieval=true&serverTimezone=UTC"   --network=bankapp   -p 8080:8080   bankapp-mini:latest
```

---



# Allow Port 8080 on AWS EC2

## 🔓 Enable Port 8080 for Public Access

1. Go to **EC2 Dashboard** → **Instances** → Select your instance.
2. Scroll to the **Security** tab → Click on the **Security Group** link.
3. Go to **Inbound Rules** → Click **Edit Inbound Rules**.
4. Click **Add Rule**:
   - **Type**: Custom TCP
   - **Port Range**: 8080
   - **Source**: 0.0.0.0/0 (for public access)

5. Click **Save Rules**.

✅ Now you can access your app at port 8080:  



## 🧪 Local Testing

After deployment, test the app using:

```
http://<your-ec2-public-ip>:8080
```

Use MySQL client or Adminer to connect to DB on port `3306`.

---

![Screenshot (1046)](https://github.com/user-attachments/assets/e1f58954-4cf6-4f70-bff0-205d731bb855)
![Screenshot 2025-07-06 102706](https://github.com/user-attachments/assets/20ee3b6a-e3a5-4899-9791-6e16162517d1)





## 📥 Download & Run Locally

You can also run the app locally without AWS:

```bash
git clone https://github.com/ajay-mall13/springboot-bankapp.git
cd springboot-bankapp
docker-compose up
```

App runs at: `http://localhost:8080`

---


---

## 🌎 Region Deployed

**AWS Region:** `us-west-1 (North California)`

---



## ✅ Conclusion

This project successfully demonstrates the deployment of a full-stack **Banking Application** using **Spring Boot** and **MySQL**, fully containerized with **Docker**, and deployed on **AWS EC2**. It showcases real-world DevOps practices such as:

- Docker-based microservice isolation  
- Secure communication between containers using Docker Bridge Network  
- Environment-based configuration for database access  
- Deployment scalability and portability via cloud infrastructure  

By eliminating Docker Compose and manually handling the network and container startup, the setup also reflects a more **hands-on approach**, giving better control over individual components.


## Key practical skills demonstrated in this project include:

- Writing and building Dockerfiles for Java applications  
- Using `docker run` with environment variables to connect backend services  
- Manually setting up Docker networks for better control over container communication  
- Deploying and exposing services over the internet using EC2

By not using Docker Compose, the project simulates real-world production scenarios where services might be started or maintained independently using orchestration tools like Kubernetes in the future.




## 🧑‍💻 Author

Ajay Mall | B.Tech ECE | SMVDU  
 





