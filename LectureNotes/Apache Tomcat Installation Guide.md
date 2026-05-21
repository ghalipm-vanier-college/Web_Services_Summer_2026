```markdown
# Jakarta EE & Apache Tomcat Setup Guide

## ✅ STEP 1 — Install Java JDK

### 🔹 Download JDK
**Recommended:** JDK 21 (stable)

Download from one of the following:
* [Oracle JDK Downloads](https://www.oracle.com/java/technologies/downloads/)
* [Eclipse Temurin JDK](https://adoptium.net/temurin/releases/)

### 🔹 Verify Installation
Open your terminal or command prompt and run:

```bash
java -version

```

**Expected Output:**

```text
java version "21"

```

---

## ✅ STEP 2 — Download Apache Tomcat

### 🔹 Download Tomcat 10

**Recommended:** Apache Tomcat 11

Download from: [Apache Tomcat Downloads](https://tomcat.apache.org/download-10.cgi)

### 🔹 Choose ZIP Version

For Windows, download either:

* **64-bit Windows zip**
* **Core zip**

---

## ✅ STEP 3 — Extract Tomcat

Extract the downloaded ZIP file to your preferred directory.

**Example location:** `C:\tomcat`

After extraction, your folder structure should look like this:

```text
C:\tomcat\bin
C:\tomcat\webapps
C:\tomcat\conf

```

---

## ✅ STEP 4 — Start Tomcat

### 🔹 Windows

1. Navigate to: `C:\tomcat\bin`
2. Double-click: `startup.bat`

### 🔹 Mac / Linux

Open your terminal in the Tomcat `bin` directory and run:

```bash
./startup.sh

```

---

## ✅ STEP 5 — Verify Tomcat Works

Open your web browser and navigate to: `http://localhost:8080`

**Expected:**
Apache Tomcat welcome page displays successfully.

---

## ✅ STEP 6 — Configure IntelliJ IDEA

### 🔹 Install IntelliJ IDEA

Download and install: [IntelliJ IDEA Community Edition](https://www.jetbrains.com/idea/download/)

### 🔹 Add Tomcat Server

1. In IntelliJ, navigate to: **File** → **Settings** → **Plugins**
2. Search for and install: **Jakarta EE**
3. Restart IntelliJ.

### 🔹 Configure Tomcat

1. Go to: **Run** → **Edit Configurations**
2. Click: **+** → **Tomcat Server** → **Local**
3. Set your Tomcat Home path: `Tomcat Home = C:\tomcat`

---

## ✅ STEP 7 — Create First Dynamic Web Project

### 🔹 New Project

1. Create a new project and choose: **Jakarta EE**
2. Add dependencies/framework specifications for: **Servlet**

---

## ✅ STEP 8 — Create First Servlet

Create a new Java class and implement your first servlet using the code below:

```java
import jakarta.servlet.annotation.WebServlet;
import jakarta.servlet.http.HttpServlet;
import jakarta.servlet.http.HttpServletRequest;
import jakarta.servlet.http.HttpServletResponse;
import java.io.IOException;

@WebServlet("/hello")
public class HelloServlet extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest request,
                         HttpServletResponse response)
            throws IOException {

        response.getWriter().write("Hello Web Services!");
    }
}

```

---

## ✅ STEP 9 — Run Application

1. Click the **Run** button in IntelliJ.
2. Open your browser and navigate to: `http://localhost:8080/your-project-name/hello`

**Expected output:**

```text
Hello Web Services!

```

---

## ⚠️ Common Problems + Fixes

### ❌ Port 8080 already in use

**Fix:**

1. Open and edit the configuration file (not in intelliJ, but in tomcat folder - such as "C:\Users\Username\apache-tomcat-11.0.22\conf"): `tomcat/conf/server.xml`
2. Change the (connector) port configuration line only (not the shutdown port):
```xml
port="8080"

```

to:
```xml
port="9090"

```
### ❌ "Port 8080 already in use" keep showing up and you do not see where it is running:
#### 1. Open cmd with **Admin privillage**, then run "netstat -ano | findstr :8080" to find the PID (number at the end)
#### 2. Run "taskkill /PID 12345 /F", if PID was 12345. Then you see:
<img width="629" height="130" alt="image" src="https://github.com/user-attachments/assets/19b35b72-8a63-4b61-826a-d2cb2198068c" />



3. Restart Tomcat and access your application at: `http://localhost:9090`

### ❌ JAVA_HOME not found

**Fix:**
Set your system environment variables to point to your JDK installation path:

```text
JAVA_HOME = C:\Program Files\Java\jdk-21

```
### ❌ Servlet runs fine, but you see "404 - Page not Found":
<img width="738" height="247" alt="image" src="https://github.com/user-attachments/assets/0345d35e-bd5a-49de-a789-8e283e3f38d9" />

#### 1. Go to Edit Configuration
<img width="1330" height="786" alt="image" src="https://github.com/user-attachments/assets/3e0e0c2f-b5e7-4af3-abe7-9b8f760abfe5" />

#### 2. Under "Server" for "Application Server", choose the Tomcat you have installed: 
<img width="1045" height="833" alt="image" src="https://github.com/user-attachments/assets/b1393bb5-59d6-4ba7-9148-b9c43bd66a94" />

#### 3. Under "Deployment", click the build artifact such as "demo:war exploded" and for "Application context", choose a name (project name is better), such as "greetings" or "demo" after a slash "/" (if URL was: http://localhost:7070/demo, then you must choose "demo" here - server URL and deployment must have same name.), then click "Apply", then click "ok". 

<img width="1045" height="799" alt="image" src="https://github.com/user-attachments/assets/6867eac1-f57d-4ed4-a47a-44b110f9584d" />

#### 4. Then run the JavaServlet application, and type "http://localhost:9090/demo/hello" into your browser. Then you should see: 
<img width="338" height="116" alt="image" src="https://github.com/user-attachments/assets/41536d7f-e99f-4f98-a655-07bb8ced8f48" />





```

```
