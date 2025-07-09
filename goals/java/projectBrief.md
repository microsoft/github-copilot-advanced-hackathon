# Project Brief: Spring Petclinic Microservices

## Overview
The **Spring Petclinic Microservices** project is a reference application based on the well-known Spring Petclinic sample, re-architected as a set of microservices. Developed and maintained by Azure Samples, it demonstrates how to build and deploy cloud-native Java applications on the Microsoft Azure platform. The application implements a full-featured veterinary clinic management system and serves as a practical example for developers.

## Purpose
The primary goals of this project are to:
- Showcase best practices for building and deploying microservices with Spring Boot and Spring Cloud on Azure.
- Demonstrate the use of **Azure Spring Apps** for hosting scalable and resilient Java applications.
- Provide a hands-on learning tool for developers exploring microservices, Infrastructure as Code (IaC), and modern DevOps practices on Azure.
- Serve as an **Azure Developer CLI (`azd`)** template for rapid, repeatable environment provisioning and application deployment.

## Key Features
- **Architecture**: A distributed microservices architecture using Spring Boot, including services for customers, vets, and visits, managed via a discovery server and an API gateway.
- **Frontend**: Built with AngularJS and Bootstrap, providing a dynamic user interface.
- **Backend**: A suite of microservices developed with Java and the Spring Framework.
- **DevOps Ready**: Includes CI/CD pipeline examples using GitHub Actions and Infrastructure as Code definitions with Bicep.
- **Cloud Integration**: Leverages key Azure services such as **Azure Spring Apps**, **Azure Database for MySQL**, and **Azure Key Vault** for comprehensive cloud-native capabilities.

## Technology Stack
- Java 17+
- Spring Boot & Spring Cloud
- AngularJS & Bootstrap
- Maven
- Docker
- Azure Spring Apps
- Azure Database for MySQL
- Azure Developer CLI (`azd`)
- Bicep

## Getting Started
To run the Spring Petclinic project on Azure:
1. Clone the repository: `git clone https://github.com/Azure-Samples/spring-petclinic-microservices.git`
2. Install prerequisites:
   - Azure Developer CLI (`azd`)
   - Java 17 SDK
   - Azure CLI
3. Run the solution on Azure using the `azd up` command, which handles provisioning and deployment.

## Use as a Reference Sample
This application is used as a public reference sample in various Microsoft tutorials, learning modules, and documentation to demonstrate how to effectively build and deploy modern Java applications on Azure. 