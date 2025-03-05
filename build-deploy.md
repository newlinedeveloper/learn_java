# **Build Tools & Deployment in Java**

Efficient **build tools and deployment strategies** are crucial for managing Java applications. This guide covers:

✅ **Build Tools:** Maven & Gradle  
✅ **Containerization:** Dockerizing Java Applications  
✅ **CI/CD Pipelines:** GitHub Actions  
✅ **Deployment:** Kubernetes  

---

## **1. Build Tools: Maven & Gradle**
Java projects use **build tools** like **Maven** and **Gradle** to manage dependencies, compile code, run tests, and package applications.

### **📌 Maven (XML-Based)**
Maven is a popular build tool that uses an **XML-based configuration** (`pom.xml`).

#### **✅ Maven Installation**
- Download and install [Apache Maven](https://maven.apache.org/download.cgi).
- Verify installation:
  ```sh
  mvn -version
  ```

#### **✅ Maven Project Structure**
```
my-app/
│── src/
│   ├── main/java/  # Source Code
│   ├── test/java/  # Unit Tests
│── pom.xml         # Maven Build Configuration
```

#### **✅ Sample `pom.xml`**
```xml
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
         http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    
    <groupId>com.example</groupId>
    <artifactId>my-app</artifactId>
    <version>1.0.0</version>
    
    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
            <version>2.7.3</version>
        </dependency>
    </dependencies>
</project>
```

#### **✅ Common Maven Commands**
```sh
mvn clean         # Clean target directory
mvn compile       # Compile Java files
mvn package       # Package JAR/WAR file
mvn test          # Run unit tests
mvn install       # Install package in local repo
```

---

### **📌 Gradle (Groovy/Kotlin-Based)**
Gradle is a powerful **build automation tool** that uses **Groovy or Kotlin DSL** (`build.gradle`).

#### **✅ Gradle Installation**
- Download and install [Gradle](https://gradle.org/install/).
- Verify installation:
  ```sh
  gradle -v
  ```

#### **✅ Sample `build.gradle` (Groovy)**
```gradle
plugins {
    id 'java'
    id 'application'
}

group = 'com.example'
version = '1.0.0'

repositories {
    mavenCentral()
}

dependencies {
    implementation 'org.springframework.boot:spring-boot-starter-web:2.7.3'
}

application {
    mainClass = 'com.example.Main'
}
```

#### **✅ Common Gradle Commands**
```sh
gradle clean      # Clean build directory
gradle build      # Build project
gradle test       # Run tests
gradle run        # Run application
```

---

## **2. Dockerizing Java Applications**
### **📌 Why Docker?**
- Ensures **consistency** across environments.
- Packages Java applications into lightweight **containers**.
- Works well with **Kubernetes** for microservices deployment.

---

### **✅ Step 1: Create a Dockerfile**
For a Spring Boot app with Maven:

```dockerfile
# Use official OpenJDK base image
FROM openjdk:17-jdk-slim

# Set working directory
WORKDIR /app

# Copy JAR file from target directory
COPY target/my-app-1.0.0.jar app.jar

# Run the application
CMD ["java", "-jar", "app.jar"]
```

---

### **✅ Step 2: Build and Run the Docker Image**
```sh
# Build Docker image
docker build -t my-app .

# Run the container
docker run -p 8080:8080 my-app
```

---

## **3. CI/CD with GitHub Actions**
### **📌 Why CI/CD?**
- Automates **testing, building, and deployment**.
- Ensures **code quality** before merging.
- Deploys applications **without manual intervention**.

---

### **✅ Step 1: Create a `.github/workflows/ci.yml` File**
```yaml
name: Java CI/CD Pipeline

on: [push, pull_request]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Set up JDK 17
        uses: actions/setup-java@v2
        with:
          distribution: 'temurin'
          java-version: '17'

      - name: Build with Maven
        run: mvn clean package

      - name: Run Tests
        run: mvn test
```

---

### **✅ Step 2: Add Docker Push to CI/CD Pipeline**
Modify `.github/workflows/ci.yml`:

```yaml
      - name: Log in to Docker Hub
        run: echo "${{ secrets.DOCKER_PASSWORD }}" | docker login -u "${{ secrets.DOCKER_USERNAME }}" --password-stdin

      - name: Build Docker Image
        run: docker build -t my-app .

      - name: Push Image to Docker Hub
        run: docker tag my-app mydockerhubusername/my-app:latest && docker push mydockerhubusername/my-app:latest
```

**🔹 Add GitHub Secrets:**
- `DOCKER_USERNAME` → Your DockerHub username.
- `DOCKER_PASSWORD` → Your DockerHub password.

---

## **4. Deploying to Kubernetes**
### **📌 Why Kubernetes?**
- Manages **scalability, load balancing, and self-healing**.
- Deploys **containerized applications** efficiently.

---

### **✅ Step 1: Create a Kubernetes Deployment**
Save as `deployment.yaml`:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app
spec:
  replicas: 2
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
      - name: my-app
        image: mydockerhubusername/my-app:latest
        ports:
        - containerPort: 8080
```

---

### **✅ Step 2: Create a Kubernetes Service**
Save as `service.yaml`:

```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-app-service
spec:
  selector:
    app: my-app
  ports:
    - protocol: TCP
      port: 80
      targetPort: 8080
  type: LoadBalancer
```

---

### **✅ Step 3: Deploy to Kubernetes**
```sh
# Apply Deployment
kubectl apply -f deployment.yaml

# Apply Service
kubectl apply -f service.yaml

# Check Deployment Status
kubectl get pods

# Get Service URL
kubectl get service my-app-service
```

---

# **🚀 Summary**
| **Step**          | **Tool/Command** |
|-------------------|-----------------|
| **Build the App** | `mvn package` / `gradle build` |
| **Dockerize App** | `docker build -t my-app .` |
| **Push to DockerHub** | `docker push my-app:latest` |
| **CI/CD Automation** | GitHub Actions |
| **Deploy to Kubernetes** | `kubectl apply -f deployment.yaml` |

---
