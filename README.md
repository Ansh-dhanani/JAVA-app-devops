# JAVA-app-devops

End-to-end **CI/CD & GitOps Pipeline on AWS** — from source-code commit to Kubernetes deployment, using Jenkins, Maven, SonarQube, Docker, Amazon ECR, Argo CD, and Amazon EKS.

## Stack

- **GitHub** — Source Control
- **Jenkins** — CI/CD Automation
- **Maven** — Build & Test
- **SonarQube** — Static Code Analysis
- **Docker** — Containerization
- **Amazon ECR** — Container Registry
- **Argo CD** — GitOps Deployment
- **Amazon EKS** — Kubernetes Orchestration

## Architecture Flow

```mermaid
flowchart TB
    DEV["Developer"]
    GH["GitHub"]
    subgraph CI["CONTINUOUS INTEGRATION"]
        direction TB
        JC["Jenkins Controller"]
        JA["Jenkins Agent"]
        MAVEN["Maven"]
        SONAR["SonarQube"]

        DOCKER["Docker"]
    end
    ECR["Amazon ECR"]
    subgraph CD["CONTINUOUS DELIVERY — GITOPS"]
        direction TB
        GITOPS["GitOps Repository"]
        ARGO["Argo CD"]
    end
    subgraph K8S["KUBERNETES"]
        direction TB
        EKS["Amazon EKS"]
        APP["Application"]
    end
    DEV --> GH
    GH --> JC
    JC --> JA
    JA --> MAVEN
    MAVEN --> SONAR
    SONAR --> DOCKER
    DOCKER --> ECR
    ECR --> GITOPS
    GITOPS --> ARGO
    ARGO --> EKS
    EKS --> APP
    classDef source fill:#161b22,stroke:#30363d,color:#fff,stroke-width:2px
    classDef ci fill:#d73a2f,stroke:#8b1e17,color:#fff,stroke-width:2px
    classDef sonar fill:#2f80ed,stroke:#1d5fa7,color:#fff,stroke-width:2px
    classDef docker fill:#2496ed,stroke:#1265a0,color:#fff,stroke-width:2px
    classDef aws fill:#ff9900,stroke:#b36b00,color:#111,stroke-width:2px
    classDef gitops fill:#6f42c1,stroke:#4c288c,color:#fff,stroke-width:2px
    classDef k8s fill:#326ce5,stroke:#1d4fa3,color:#fff,stroke-width:2px
    class DEV,GH source
    class JC,JA,MAVEN ci
    class SONAR sonar
    class DOCKER docker
    class ECR,EKS aws
    class GITOPS,ARGO gitops
    class APP k8s
```

## Pipeline

1. The application source code is pushed to GitHub, triggering Jenkins.
2. Jenkins builds and tests the application with Maven, performs static code analysis with SonarQube, builds the Docker image, and pushes it to Amazon ECR.
3. The Kubernetes manifests are maintained in a GitOps repository. Argo CD monitors the repository and synchronizes the declared state with the Amazon EKS cluster.
4. The application is then deployed and managed as Kubernetes workloads running on EKS.

**Flow:** GitHub → Jenkins → Maven → SonarQube → Docker → Amazon ECR → GitOps Repository → Argo CD → Amazon EKS → Application

## Infrastructure

- Jenkins Controller
- Jenkins Agent
- Amazon EC2
- Amazon EKS / Kubernetes workloads
- GitOps repository

## Goal

Demonstrate an end-to-end CI/CD + GitOps workflow on AWS, from source-code commit to Kubernetes deployment.