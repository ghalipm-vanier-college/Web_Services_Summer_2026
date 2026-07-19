# WSDL, SOAP: Modern Perspective
---

# Session 1 – SOAP Web Services

## Old Approach

> Today we learn SOAP.

> "Why are we learning this? Everybody uses REST."

---

## Modernized Approach

Evolution of Web Services:

```
1998–2010

SOAP
        ↓

2010–Today

REST APIs
        ↓

Today

REST + GraphQL + gRPC
```

Then explain:

> Although REST dominates new development, many banks, insurance companies, airlines, hospitals, governments, and ERP systems still expose SOAP services.
> As a developer, you may need to integrate with these systems.

Now SOAP has a purpose.

---

## When SOAP is Still Used


Examples

```
Bank payment systems

Airline reservation systems

Insurance companies

Government services

SAP ERP

Oracle ERP
```

So we understand why SOAP still exists.

---

## Comparison of REST and SOAP



| REST            | SOAP                           |
| --------------- | ------------------------------ |
| JSON            | XML                            |
| Lightweight     | Verbose                        |
| HTTP methods    | Usually POST                   |
| Easy to consume | Strict contract                |
| Mobile friendly | Enterprise integration         |
| Most new APIs   | Many legacy enterprise systems |

Already knowing REST, so SOAP becomes much easier to understand.

---

## Demonstration

Start with a REST request.

```
GET

/students
```

JSON response

↓

Then show SOAP.

```
POST

/soap
```

SOAP XML request

↓

SOAP XML response

We immediately see the difference.

---

## WSDL

Instead of saying

> WSDL is an XML file.

We say

> WSDL is the API documentation for a SOAP service.

We already know

```
Swagger/OpenAPI
```

Now compare them.

| REST            | SOAP |
| --------------- | ---- |
| Swagger/OpenAPI | WSDL |

That makes WSDL much easier to understand.

---

## SoapUI

Instead of saying

> SoapUI sends SOAP requests.

Compare it with Postman.

| REST    | SOAP   |
| ------- | ------ |
| Postman | SoapUI |

We already know Postman.

Learning SoapUI becomes much easier.

---

# Lab

build

```
College Registration SOAP Service
```

Operations

```
Find College

Add College

Delete College

List Colleges
```

Much closer to their REST projects.

---

# Session 2 – JSON/XML Annotations

This topic can be modernized even more.

---

## Old Approach

Covering

```
@JsonProperty

@XmlElement

@XmlRootElement
```

Students memorize annotations.

---

## Modern Approach

Start with a question.

```
Can one REST endpoint return both JSON and XML?

```
GET

/students
```

Request Header

```
Accept: application/json
```

↓

JSON returned.

---

Same endpoint

```
GET

/students
```

Header

```
Accept: application/xml
```

↓

XML returned.

Not surprising.


---

## Introduce Content Negotiation

Spring Boot chooses the output format based on the client's `Accept` header.

```
Client

↓

Accept: application/json

↓

JSON
```

or

```
Client

↓

Accept: application/xml

↓

XML
```

This is called **Content Negotiation**.

Now annotations have a purpose.

---

## Jackson

Instead of listing annotations, we show what each one changes.

Before

```json
{
  "studentName":"Alice"
}
```

After

```java
@JsonProperty("name")
```

↓

```json
{
   "name":"Alice"
}
```

Students see the effect immediately.

---

## XML

Same idea.

Before

```xml
<Student>
```

After

```java
@XmlRootElement(name="Learner")
```

↓

```xml
<Learner>
```

Students immediately understand the annotation.

---

## Master-Detail

Instead of abstract examples, use their existing database.

```
College

↓

Students
```

One college

Many students

Return

```json
{
   "id":1,

   "name":"Vanier",

   "students":[

      ...

   ]
}
```

One can do this in XML. Understand the relationship.

---

# Updated Lab

Instead of creating a new project,

extend the existing Spring Boot application.

```
College

↓

Students
```

Return

JSON

↓

Switch header

↓

Return XML

↓

Modify annotations

↓

Observe output changes

Students see how annotations directly affect serialization.

---

# Add One New Modern Topic (10 minutes)

At the end of the session, briefly introduce **OpenAPI/Swagger**.

Students already know:

```
REST

↓

JSON

↓

Spring Boot
```

Show them that professional REST APIs are often documented with Swagger.

```
Browser

↓

Swagger UI

↓

Try GET

↓

JSON returned
```

They don't need to build it—just seeing it prepares them for industry tools.

---

# Recommended Flow

## Session 1 (SOAP)

1. Evolution of Web Services (SOAP → REST)
2. Why SOAP still exists
3. SOAP architecture
4. SOAP message
5. WSDL (compare with Swagger/OpenAPI)
6. SoapUI (compare with Postman)
7. Spring Boot SOAP service
8. Hands-on lab

---

## Session 2 (JSON/XML)

1. JSON vs XML
2. Content Negotiation (`Accept` header)
3. Jackson annotations
4. JAXB/XML annotations
5. Master-detail relationships
6. Nested JSON and XML
7. Spring Boot serialization
8. Hands-on lab

