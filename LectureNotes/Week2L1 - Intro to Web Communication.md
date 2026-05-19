# Lecture: Web Services and Inter-Process Communication

## 1. Introduction to Web Services
Web services are modular, platform-independent software applications that bridge the gap between disparate technologies. They enable seamless interoperability across different programming languages and operating systems.

### Core Function & Interoperability
* **Standardized Bridge:** Facilitates communication between heterogeneous systems.
* **Universal Compatibility:** Allows applications built in Java, Python, C#, or PHP to exchange information via open web standards.

### Key Technical Components
* **Transport Layer:** HTTP/HTTPS protocol for sending requests and responses.
* **Data Format:** XML or JSON used to structure transmitted data.
* **Service Description:** WSDL (Web Services Description Language) documents define service capabilities and communication requirements.



---

## 2. Inter-Process Communication (IPC)
IPC refers to the mechanisms an operating system provides to allow separate, isolated processes to coordinate and exchange data.

### Primary Models of IPC
| Model | Mechanism | Key Characteristic |
| :--- | :--- | :--- |
| **Shared Memory** | Processes access a common memory space. | Extremely fast; requires synchronization to avoid collisions. |
| **Message Passing** | Data is exchanged via OS-managed channels/queues. | Safer; decoupled from memory management. |

### Web Services as a Form of IPC
Web services can be viewed as an extension of IPC that operates **across a network**. While traditional IPC occurs within a single host, web services allow processes on completely different machines to collaborate.

---

## 3. Client/Server Communication Model
A distributed computing architecture that divides tasks between two independent entities: the **Requester (Client)** and the **Provider (Server)**.

### The Workflow Cycle
1. **Request:** The client establishes a connection and transmits a structured request.
2. **Processing:** The server receives the request, performs business logic, or queries a database.
3. **Response:** The server sends a formatted response back to the client for final display or processing.
