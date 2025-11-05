# Self Evaluation

## Requirements

1. Set up a Kubernetes cluster (you can use a local tool like Minikube or a cloud-based service like GKE, EKS, or AKS).

    ```text
    I used podman desktop and kind to create the Kubernetes cluster on my machine because I didn't have access to a public cloud.
    
    I think podman was a sensible choice over docker desktop due to the business license restrictions imposed by Docker for businesses using their tool.
    
    If I had access to a public cloud I would have opted to use AWS because it's what I am most familar with.

    I would have then used terraform/opentofu with community terraform modules to produce the following:
    
     - VPC with 3 tiers (public, private and data) across 2 availibility zones
     - ALB Load Balancer inside the public subnets
     - EKS Kubernetes cluster inside the private subnets
     - RDS Postgres Database instances inside the data subsets
    ```

2. Consider using deployment templating tools like Helm, Kustomize, Jsonnet, or similar, for managing Kubernetes manifests and configurations. Explain your choice. 

    ```text
    I used helm because I like following benifits over something like kustomize: 
    
    - Charts bundle all necessary manifests (Deployments, Services, Ingresses, ConfigMaps, etc.) into a single logical unit. This simplifies the deployment and sharing of applications.

    - Helm is very popular tool so many people are familar with it and are able to support and work with it, which can be important when scaling up a team or operations.

    - Helm is strongly well supported in k8s eco system for example ArgoCD applications.
    ```
3. Create YAML manifests for deploying the two services (main, database) in
Kubernetes using your chosen deployment templating tool.

    ```text
    Charts:

    I created two helm charts, 1 to deploy vikunja and 1 to deploy postgres database.

    Note: I was informed this didn't have to be production ready, this postgres deployment couldn't be further from production ready. For one the data isn't persisted. I would have prefered to use managed services for databases. See 4. for more jsutification.

    Manifests:

    I created a postgres.secret.yaml manifest for storing postgres secrets for the application. The reason I seperated this from the helm charts is because in a production like environment, this would be managed with kubeseal and argocd (GitOps approach).

    ```

4. Consider whether the database service should be self-hosted or managed (e.g., selfhosted PostgreSQL vs. managed database service like AWS RDS or Google Cloud
SQL). Justify your choice.

    ```text
    See: docs/managed-vs-self-hosted.md

    ```
5. Optionally, implement Identity and Access Management (IAM) for secure

    ```text
    Not complete. Ran out of time before I go on holiday.

    ```

6. Ensure that the Vikunja ToDo List application is highly available and resilient to failures.

    ```text
    - Replicas set to more then 1
    - Readiness endpoint configured to stop requests hiting unready pods
    - podAntiAffinity set to stop pods  with matching labels from being scheduled in the same AZ
    - Database should be highly availible (not in my case, explained many times)
    ```

7. Implement and configure a load balancer to distribute traffic across the services.

    ```text
    Handled by Ingress Controller but there are many benifits to using managed services like AWS ALB.

    - Spend less time managing infrastructure and more time on business problems
    - Security with minimal setup i.e. ddos protection/waf.
    - Out of the box monitoring and metrics
    ```

8. Optimize the network settings for low latency and high throughput.

    ```text
    Nodes:

    I used a daemonset to tune the underlying nodes, it can be found here: manifests/sysctl-tuner.daemonset.yaml

    An alternative solution would be to use something like a launch template script to run on the nodes at start up.

    Pods:
    
    Docs: https://kubernetes.io/docs/tasks/administer-cluster/sysctl-cluster/#setting-sysctls-for-a-pod

    PS: If I am being honest, this isn't an area I am confident in.
    ```

9. Use any necessary tools or configurations to monitor and debug the application. 

    ```text
    Ran out of time to implement anything robust. However, I implemented a few scripts in taskfile common tasks locally.

    - task app:ping - Which connects verifies the application is running and availible via the service.
    - task app:logs - Which follows the deployment logs for the application.

    In a production environment I would consider the following:

    - Implementation of a log agregation and storage system for tracability and analysis, something like splunk, greylog or elk
    - Monitoring of pods and node status, to be notified when pods go unhealthy or can't be scheduled, promethous, signalfx, datadog or cloud provider solution.
    - Some sort of external uptime monitoring, making sure the app is reachable from the wider internet, something like pingdom
    - You could also implement something like open telemetry collector and ship traces and custom metrics from application to external platform
    ```

# Evaluation Criteria

* Proper usage of Kubernetes resources (Deployments, Services, Pods, etc.)
through your chosen deployment templating tool.

  ```
  See charts/vikunja/templates

  or

  Generate the manifests using "task app:manifests"
  ```

* Efficient resource utilization (e.g., defining resource limits and requests).

  ```
  See: charts/vikunja/local.values.yaml
  ```

* Implementation of health checks and readiness probes for services.

  ```
  See: charts/vikunja/local.values.yaml
  See: charts/postgres/local.values.yaml
  ```


* Effective use of deployment templating tool for configuration management.

  ```
  See: charts/vikunja
  ```

* Demonstrated knowledge of network optimization techniques.

  ```text
  See: manifests/sysctl-tuner.daemonset.yaml
  See: charts/vikunja/local.values.yaml

  PS: Not confident on this one, but I have given it ago. In a real world environment I think it would make sense to replicate the setup and produce some load on a system before applying these changes to production.
  ```

* Justification and implementation of database deployment strategy (self-hosted
vs. managed).

  ```text
  See: docs/managed-vs-self-hosted.md
  ```

* Optional: Correct implementation of Identity and Access Management using
Keycloak for secure authentication and authorization.

  ```text
  Not implemented, ran out of time.
  ```