---
layout: ../layouts/AboutLayout.astro
title: "About"
---

# Software Engineer

Software Engineer with strong experience in Spring Boot and Spring Cloud microservices, building secure, production-grade REST APIs for transaction monitoring and payment systems. Skilled in schema-based multitenancy using Hibernate JPA, PostgreSQL performance optimization, and access-token security enforcement at the API gateway level. Hands-on experience with CI/CD pipelines, Docker, Helm, and Azure Kubernetes Service (AKS), along with centralized logging and observability using ELK, Prometheus, and Grafana. Proven ability to troubleshoot and resolve production-critical issues in high-availability environments.

## Experience

### **Software Engineer at In-Solutions Global Ltd**

June 2022 - Present Mumbai

#### Spring Boot API Development

* Developed production-grade Spring Boot REST APIs with Spring MVC, Spring Data JPA, Hibernate, and layered architecture, using DTOs, ModelMapper, and Lombok for clean, maintainable code.
    
* Implemented consistent API responses, global exception handling with @RestControllerAdvice for reliability and testability
    
* Developed Spring Boot APIs for transaction monitoring dashboards.
    
* Built payment-link generation APIs to route transactions between Lyra, TPSL, PayU.
    
* Created APIs handling Amex Target Transaction calls via SOCKS proxy for POS and PG JPMC flows.
    
* Developed scheduled Spring Boot jobs to sync transaction data from database → Redis, exposing APIs for real-time monitoring performance dashboards.
    

#### Multi-Tenancy & Database Architecture

* Implemented schema-based multitenancy using Hibernate JPA, allowing a single Spring Boot application to serve multiple clients with isolated data per schema.
    
* Developed and optimized complex PostgreSQL join queries across multiple tables to efficiently retrieve transaction and payment data, working with both development and production environments.
    

#### Spring Cloud Microservices Architecture

* Implemented microservices ecosystem using Spring Cloud Gateway, Eureka service discovery, and Nginx for secure routing, dynamic service resolution, and controlled API exposure.
    
* Designed and implemented an access-token validation filter in Spring Cloud Gateway, resolving a production issue where public requests could access microservices without authentication.
    
* Developed access-control components including token filters, LLT checks, bypass rules, and worked with SOCKS proxy tunneling to support secure internal communication between services.
    
* Configured Nginx as forward/reverse proxy with SSL termination, domain routing, rewrite rules, routing public traffic Nginx → Gateway → Microservices to ensure secure and efficient request flow.
    

#### CI/CD, Containerization & Cloud Deployment (Jenkins, Docker, Helm, AKS)

* Built Jenkins pipelines for Spring Boot microservices to build JARs using Maven, create Docker images, and push images to the Nexus Docker Registry using tag-based versioning for consistent deployment flow.
    
* Automated Helm chart updates and deployments to Azure Kubernetes Service (AKS), and managed supporting infrastructure including Redis, Kafka, and Postgres provisioned on Azure VMs to support microservice environments.
    
* Used Docker Compose to spin up isolated test environments with Kafka, Redis, database, and application containers, and used Prometheus and Grafana to enhance service observability.
    

#### ELK Logging & Observability

* Implemented Elastic + Logstash integration for 3 microservices.
    
* Streamed logs and metrics to Kibana dashboards for client-specific diagnostics (JPMC, Yes Bank).
    
* Improved incident analysis and reduced debugging time.

## 🛠 Skills & Tech Stack

### 💻 Languages
- Java
- JavaScript
- SQL

### ⚙️ Frameworks & Core Concepts
- Spring Boot
- Spring Cloud
- Spring MVC
- Hibernate / JPA
- REST API Design
- Core Java, OOP, Collections, Exception Handling

### 🧩 Microservices & Networking
- Eureka Service Discovery
- Spring Cloud Gateway
- Nginx (Reverse / Forward Proxy)
- SSL, Networking Concepts

### 🚀 DevOps & CI/CD
- Jenkins
- GitHub CI
- Docker
- Kubernetes & Helm
- Nexus Repository

### ☁️ Cloud Platforms
- AWS
- Azure (AKS)
- OCI

### 🗄 Databases & Caching
- PostgreSQL
- Redis
- Database Sharding
- Schema-Based Multitenancy

### 📊 Monitoring & Logging
- ELK Stack (Elasticsearch, Logstash, Kibana)
- Prometheus
- Grafana

### 🧰 Tools & Practices
- Git
- Agile / Scrum
- Vim
- VS Code
- IntelliJ IDEA
- ChatGPT

## 📜 Certifications

- **AWS Certified Cloud Practitioner**  
  *Issued: June 30, 2024*

## 🎓 Education

**Bachelor of Engineering, Computer Science**  
*University of Mumbai* | GPA: 8.68  
*June 2018 – May 2022*


## Socials

[LinkedIn](https://www.linkedin.com/in/pratik280/) | [My Website](https://pratik280.github.io/) | [Github](https://github.com/Pratik280) | [Twitter](https://twitter.com/pratikchandlekr) | [Frontend Mentor](https://www.frontendmentor.io/profile/Pratik280) | [findcoder.io](https://www.findcoder.io/u/pratik280)
