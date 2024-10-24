# Spring PetClinic Cloud Microservices - DevOps Modernization Project

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

The initial PetClinic application served as a legacy microservices-based Java system that, while functional, did not adhere to modern DevOps practices. As a result, the application struggled with scalability, and the software development lifecycle was ripe for optimization. This project aims to transform the original system into a cloud-native application by leveraging modern DevOps tools and methodologies.

## Key Technologies Used

- AWS Cloud: Provides hosting and infrastructure services.
- Kubernetes (EKS): Manages microservices orchestration.
- Helm Charts: Facilitates application deployment on Kubernetes.
- Jenkins: Implements Continuous Integration (CI).
- ArgoCD: Automates Continuous Deployment (CD) with a GitOps approach for Kubernetes manifests.
- Terraform: Utilizes Infrastructure as Code (IaC) principles.
- Prometheus & Grafana: Enables monitoring and alerting.
- Velero: Offers backup solutions for Kubernetes resources.

[See the presentation of the Spring Petclinic Framework version](http://fr.slideshare.net/AntoineRey/spring-framework-petclinic-sample-application)

## Implementation Details

### 1. Infrastructure as Code (IaC) with Terraform
Using Terraform, we provisioned a resilient AWS infrastructure that includes:

- VPC Configuration: Designed with both public and private subnets to enhance security and isolation.
- EKS Cluster Deployment: Shipped in private subnets to ensure optimal connectivity and security practices.
- Multi-AZ RDS Database: Configured for high availability and quick recovery.
- Additional Tools: Helm, Velero, Prometheus, and Grafana were integrated into the architecture.

To facilitate team collaboration, Terraform backend storage is managed via an S3 bucket, with all IaC code housed in the terraform branch of the repository.

## 2. Continuous Integration (CI) Pipeline
Our team developed a Jenkins CI pipeline that automates:

- Build & Test Processes: The application is built and tested within Docker containers to ensure consistency and reliability.
- Image Management: Successfully pushes Docker images to private ECR repositories for secure storage.
- Automatic Updates: Ensures Kubernetes manifests are updated with the latest image tags to reflect the most current application version.

## 3. Continuous Deployment (CD) Pipeline

Utilizing ArgoCD, we established a streamlined deployment process:

- GitOps Integration: ArgoCD monitors our Kubernetes repository via webhooks, automatically deploying updated images to the staging environment.
- Manual Production Deployment: For production environments, deployments require manual approval—maintaining an essential layer of oversight.
- Real-Time Monitoring: ArgoCD provides up-to-date insights on service health, ensuring the application runs smoothly.

## 4. DNS and Secure HTTPS Configuration

Using AWS Route 53, we configured our domain (https://petclinicdev.online/) to manage traffic efficiently:

- Ingress LoadBalancer: Routes external traffic into the EKS cluster.
- SSL Encryption: An SSL certificate from AWS Certificate Manager ensures secure HTTPS connections for all users.

## 5. Enhanced Monitoring and Alerts
To maintain performance visibility:

- Prometheus Metrics: We implemented Prometheus to gather metrics from the EKS cluster.
- Grafana Dashboards: These metrics are visualized using Grafana, allowing us to track performance metrics like CPU usage in real time.
- Alerting Mechanism: Notifications are sent to our team via Slack whenever key performance indicators exceed predefined thresholds, allowing for quick responsiveness.

## 6. Comprehensive Backup Policy
To safeguard our data, we leveraged Velero for backup management:

- Daily Backups: Velero creates daily backups of our Kubernetes resources at 3 AM for both staging and production environments.
- RDS Automated Backups: AWS RDS features ensure point-in-time recovery through automated snapshots to protect against data loss or failures.


## Conclusion
This project exemplifies the successful implementation of modern DevOps tools and practices, transforming a legacy Java application into a scalable, cloud-native system. By utilizing AWS, Kubernetes, and a GitOps approach, we have not only enhanced the scalability and performance of the PetClinic application but also laid the foundation for a more efficient and reliable software development lifecycle. 

Follow along as we continue to refine our practices and explore innovative solutions in the ever-evolving world of DevOps!
