# Case Study

We would like to extend our congratulations on your successful completion of the initial technical interview for the DevOps Engineer position at Distribusion. Your demonstrated skills and expertise were truly impressive.

As you prepare for the upcoming second round of interviews, we have included a case study exercise which will play a crucial role in our discussions. You are welcome to prepare either a partial or full solution in advance.

During the interview process, our focus will be on two key aspects. Firstly, we will expect a thorough walkthrough and presentation of your solution. Additionally, we will request that you make a minor adjustment to the solution, allowing us to assess your adaptability and problem-solving skills.

Once again, congratulations on your progress thus far. We are enthusiastic about the opportunity to further explore your expertise in our upcoming meeting. Should you have any questions or require additional clarification on any matter, please do not hesitate to reach out.

**Task:** Todo App

**Scenario:** You have been given the Vikunja ToDo List application ([link](https://vikunja.io/)), a
microservices-based app that consists of two services: main, and database. Your task is to automate the deployment of this application using Kubernetes, optimize the network configuration for performance and reliability, consider the deployment strategy for the database service, and optionally implement Identity and Access Management (IAM) using Keycloak for secure authentication and authorization.

## Requirements

1. Set up a Kubernetes cluster (you can use a local tool like Minikube or a cloud-based service like GKE, EKS, or AKS).
2. Consider using deployment templating tools like Helm, Kustomize, Jsonnet, or
similar, for managing Kubernetes manifests and configurations. Explain your choice.
3. Create YAML manifests for deploying the two services (main, database) in
Kubernetes using your chosen deployment templating tool.
4. Consider whether the database service should be self-hosted or managed (e.g., selfhosted PostgreSQL vs. managed database service like AWS RDS or Google Cloud
SQL). Justify your choice.
5. Optionally, implement Identity and Access Management (IAM) for secure
authentication and authorization using Keycloak.
6. Ensure that the Vikunja ToDo List application is highly available and resilient to failures.
7. Implement and configure a load balancer to distribute traffic across the services.
8. Optimize the network settings for low latency and high throughput.
9. Use any necessary tools or configurations to monitor and debug the application. 

## Evaluation Criteria

* Proper usage of Kubernetes resources (Deployments, Services, Pods, etc.)
through your chosen deployment templating tool.

* Efficient resource utilization (e.g., defining resource limits and requests).
* Implementation of health checks and readiness probes for services.
* Effective use of deployment templating tool for configuration management.
* Demonstrated knowledge of network optimization techniques.
* Justification and implementation of database deployment strategy (self-hosted
vs. managed).
* Optional: Correct implementation of Identity and Access Management using
Keycloak for secure authentication and authorization.

## Deliverables

1. YAML manifests for deploying the services (main.yaml, database.yaml) using
your chosen deployment templating tool.
2. Explain your choice of using the deployment templating tool, and how it was
leveraged for configuration management.
3. A brief documentation explaining your design decisions, any optimizations
made, the justification for the database deployment strategy, and optionally,
details on Keycloak IAM setup.
4. Optional: A script or automation tool for monitoring or troubleshooting the
Vikunja ToDo List application.
