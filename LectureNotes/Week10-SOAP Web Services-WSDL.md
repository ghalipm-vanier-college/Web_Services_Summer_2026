
1. **SOAP Web Services (HTTP Methods + WSDL + SOAP UI)**
2. **JSON/XML Annotations & Master-Detail Report**

---

# Session 1 (30 min Lecture + 2 hr Lab)

## SOAP Web Services with Spring Boot

### 30-Minute Lecture

* What is SOAP?
* SOAP vs REST
* SOAP Architecture
* SOAP Message Structure
* WSDL (What is it? Why is it needed?)
* Creating SOAP Services using Spring Boot
* Testing SOAP Services with SoapUI
* HTTP POST in SOAP
* Advantages and disadvantages of SOAP

---

### 2-Hour Lab

Students build a SOAP Web Service.

Project:

```
College SOAP Service
```

Operations

```
getCollege()

getAllColleges()

addCollege()
```

Students will

* Create Spring Boot SOAP project
* Configure WSDL
* Generate Java classes from XSD
* Create Endpoint
* Test using SoapUI
* Examine SOAP Request
* Examine SOAP Response
* Modify the service

---

# Session 2 (30 min Lecture + 2 hr Lab)

## JSON/XML Annotations & Master-Detail Report

### 30-Minute Lecture

* JSON serialization
* XML serialization
* Jackson annotations

```
@JsonProperty

@JsonIgnore

@JsonFormat

@JsonInclude
```

* JAXB annotations

```
@XmlRootElement

@XmlElement

@XmlAttribute

@XmlTransient
```

* Producing JSON

* Producing XML

* Master-Detail relationships

```
College

↓

Students
```

* Nested JSON

* Nested XML

---

### 2-Hour Lab

Students create

```
College

↓

Many Students
```

REST API

```
GET /college

GET /college/{id}
```

Return

JSON

and

XML

using annotations.

Topics need to be covered:

* One-to-Many mapping
* Nested JSON
* Nested XML
* Jackson
* JAXB
* Postman testing

---

SOAP is now primarily encountered in **legacy enterprise systems**, while most new development uses REST. 
SOAP is an important technology that may show up when maintaining or integrating with existing systems, 
rather than the default choice for new APIs.

Similarly, for the JSON/XML session, rather than focusing only on annotations, emphasize **content negotiation** in Spring Boot. 
One can show how the same controller can return either JSON or XML based on the client's `Accept` header, with annotations controlling 
the serialization format. This helps one to understand a practical feature in real Spring Boot applications 
while still covering the required JSON/XML annotations.
