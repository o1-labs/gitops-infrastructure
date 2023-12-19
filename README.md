# Continuous Deployment Infrastructure Documentation for the Platform Engineering Team

## Overview

Welcome to the `gitops-infrastructure` GitHub repository. This repository is an embodiment of our commitment to GitOps-based Continuous Deployment (CD) practices. It's meticulously designed to mirror a filesystem-like structure, which not only aligns with our CD workflow but also reinforces the principles of GitOps. The primary aim of this structure is to achieve an efficient and clear decoupling of domains within our deployment process. 

Key aspects of this design include:

- **Reflecting GitOps Principles**: The repository structure is a direct reflection of our CD process. By adhering to GitOps best practices, it ensures that the entire deployment lifecycle is manageable through Git. This approach enables us to have a single source of truth for our infrastructure and applications, making the deployment process transparent and auditable.

- **Efficient Decoupling of Domains**: We have strategically divided the repository into separate directories, each serving a distinct purpose. This separation facilitates better organization, easier management, and a clearer understanding of each domain within our deployment pipeline.

    - **`argocd/` Directory**: Houses the ArgoCD deployment configuration and the application Seeder. This setup allows us to manage the ArgoCD environment and its bootstrap process independently, ensuring a clean separation between the deployment tooling and the applications being deployed. Check the [README.md](./argocd/README.md) to understand how to onboard a new Application or Cluster.

    - **`applications/` Directory**: Dedicated to ArgoCD Applications and ApplicationSets. This separation makes Applications' orchestrate isolated baseline Helm Charts, making them easier to manage and scale.

    - **`charts/` Directory**: Contains the baseline Helm Charts for applications. By decoupling these charts, we establish a clear baseline for application deployments, ensuring consistency across various environments.

    - **`platforms/$CLUSTER/$APP/values.yaml` Hierarchy**: This unique structure provides an isolated and specific configuration for each deployment, segmented by cluster and application. Such a hierarchy not only simplifies the management of different environments but also allows anyone to understand the current state of the clusters by simply reviewing the repository.

The `gitops-infrastructure` repository is not just a collection of files and directories; it's a reflection of our strategic approach to Continuous Deployment. By leveraging GitOps and organizing our repository to mirror our CD process, we've created a system that is efficient, transparent, and scalable. This repository is central to understanding and participating in our deployment processes as a member of the Platform Engineering Team.

### Workflow Integration

The repository's structure is integral to our CD workflow. By leveraging tools like Argo CD and Helm, combined with the clearly defined directory structure, we create a robust and scalable deployment environment. This setup facilitates:
- **Automated Deployments**: Changes in the repository trigger automated deployment processes, ensuring that our infrastructure is always up-to-date with the latest configurations.
- **Clarity and Consistency**: The logical separation of components within the repository makes it easier for team members to understand and contribute to different aspects of the infrastructure.
- **Scalability**: The use of patterns like 'app of apps' and generators allows for scalable management of multiple applications and environments.
---

This document is a living piece of our infrastructure; updates and improvements are welcomed and encouraged. For more detailed information on each component, refer to the respective directories within the repository.