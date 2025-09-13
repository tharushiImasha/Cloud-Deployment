# Deployment in GCP

## 🌟 Project Overview
This repository showcases my hands-on assignment for **Enterprise Cloud Architecture**. The project illustrates the deployment of a Spring Boot application with MySQL database integration using Google Cloud SQL services.

## 🎥 Demo Video
Check out the demonstration: [See Video Here](https://drive.google.com/file/d/1cf-tT1DuZvZPCbYVRA09GexqSfRob5np/view?usp=sharing)

## ⚙️ Google Cloud MySQL Database Configuration Guide

### Phase 1: Access Google Cloud Console
* Navigate to: https://console.cloud.google.com/sql
* Verify you're working within the correct project environment.

### Phase 2: Initialize Cloud SQL Instance
1. Select **Create Instance** → opt for **MySQL**.
2. Select **MySQL 8.0** (strongly recommended).
3. Assign an **Instance ID** (example: `mysqldb-instance`).
4. Configure the **root password** (example: `Mysql-ECA1!`).
5. Region selection: choose **us-central1** (or your nearest region).
6. Availability configuration: select **Single zone** for development purposes.

### Phase 3: Configure Public IP Access
1. Navigate to your instance → select **Connections** section.
2. Under **Public IP**, select **Add network**.
3. Provide name: `development-access`.
4. Set IP range to `0.0.0.0/0` (⚠️ **Development use only**).
5. Save configuration and note down the **Public IP** (example: `34.135.121.174`).

### Phase 4: Database Creation Within Instance
1. Launch Cloud Shell or local terminal and establish connection:

```bash
docker run -it --rm mysql:8 mysql -h <YOUR_PUBLIC_IP> -u root -p
```

Example connection:

```bash
docker run -it --rm mysql:8 mysql -h 34.57.148.206 -u root -p
```

Enter your configured password (`Mysql-ECA1!`).

2. Execute database creation command:

```sql
CREATE DATABASE eca_courses;
```

3. Verify successful creation:

```sql
SHOW DATABASES;
```

The `eca_courses` database should appear in the list.

### Phase 5: Spring Boot Application Integration
Configure your `application-gcp.properties` file:

```properties
spring.datasource.url=jdbc:mysql://<Public IP address>:3306/eca_courses?createDatabaseIfNotExist=true
spring.datasource.username=root
spring.datasource.password=#######
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true

server.port=8081
```

Launch your Spring Boot application to establish connection with the Cloud SQL database.

## 🚀 Getting Started

1. Clone this repository:

```bash
git clone https://github.com/tharushiImasha/Cloud-Deployment.git
```

2. Modify `application-gcp.properties` with your specific database configuration.
3. Execute the Spring Boot application:

4. Open your browser and navigate to `http://localhost:8081`.


## 📄 License Information
This project is distributed under the [MIT License](LICENSE).. 
