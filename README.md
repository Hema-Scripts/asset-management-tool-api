# Asset Management Tool

## Overview
---

## Issues Faced During Setup

### 1. Lombok Build Failure

#### Problem

While compiling the project using:

```bash
mvn clean compile
```

multiple compilation errors were generated:

```text
cannot find symbol
getAssetName()
getStatus()
getLocation()
getSerialNumber()
```

#### Root Cause

The project was configured for:

* Java 17
* Spring Boot 2.7.0
* Lombok

However, the system was running:

```text
Java 25
```

Lombok annotation processing was not compatible with the current environment setup.

#### Resolution

Switched from Java 25 to Java 17.

No code modifications were required in:

* AssetsDto.java
* AssetsEntity.java
* CountOfAssetsEntity.java

---

### 2. Running the Project Using JDK 17

#### JDK Location

```text
PATH\jdk-17.0.12
```

#### Commands

```powershell
$env:JAVA_HOME="PATH\jdk-17.0.12"

$env:PATH="$env:JAVA_HOME\bin;$env:PATH"
```

#### Verify Version

```powershell
java -version
mvn -version
```

Expected:

```text
Java 17.0.12
```

---

### 3. Successful Compilation

Command:

```bash
mvn clean compile
```

Output:

```text
BUILD SUCCESS
```

---

### 4. MySQL Connection Failure

#### Error

```text
Communications link failure
Connection refused
```

#### Root Cause

MySQL server was not installed.

#### Resolution

Installed:

```text
MySQL 8
```

Installation Options:

```text
Setup Type: Full
Authentication: Use Strong Password Encryption
```

---

### 5. Database Configuration

File:

```text
src/main/resources/application.properties
```

Configuration:

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/assetdb?createDatabaseIfNotExist=true&useSSL=false&allowPublicKeyRetrieval=true
spring.datasource.username=root
spring.datasource.password=root
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
```

Database Creation:

```sql
CREATE DATABASE assetdb;
```

---

### 6. Flyway Migration

Flyway was configured to execute database migrations automatically during application startup.

Result:

```text
Flyway migration executed successfully
```

Database tables were created automatically.

---

## Running the Application

### Development Mode

```powershell
$env:JAVA_HOME="PATH\jdk-17.0.12"

$env:PATH="$env:JAVA_HOME\bin;$env:PATH"

mvn spring-boot:run
```

---

### Compile Project

```bash
mvn clean compile
```

---

### Build JAR

```bash
mvn clean package -DskipTests
```

---

### Run JAR

```bash
java -jar target\assetmanagementtool-0.0.1.jar
```


---

## Important Files

```text
pom.xml
application.properties
AssetsDto.java
AssetsEntity.java
CountOfAssetsEntity.java
JwtAuthenticationController.java
AdminServiceImpl.java
JwtUserDetailsServie.java
JwtRequestFilter.java
```

---

