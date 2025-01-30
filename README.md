<div align="center">
  <h1>LEDGERLY</h1>
</div>

# ARCHITECTURE
![Ledgerly_Project](https://github.com/user-attachments/assets/15bc4476-d759-4365-b787-f7ea3d47862e)

# Expense Tracker API System

## Overview
This repository contains the architecture and implementation details of an Expense Tracker API system deployed on AWS Cloud. The system leverages various AWS services and Docker containers to provide a scalable and efficient solution for tracking expenses through receipt images.

## System Architecture
The system architecture is illustrated in the diagram above. Here is a detailed description of each component and its role in the system:

1. **AWS Cloud (ap-south-1, Mumbai):** The entire system is hosted on the AWS Cloud in the Mumbai region.

2. **Amazon Simple Storage Service (S3):** Users upload receipt images to an S3 bucket. When an object (receipt image) is created in S3, it triggers an event notification.

3. **S3 Event Notification:** The creation of an object in S3 triggers an event notification, which in turn triggers a Lambda function.

4. **Receipt OCR Lambda Container:** The Lambda function processes the receipt image by feeding it to the Gemini Vision Model API, which extracts the receipt data.

5. **Gemini 1.5 Flash Vision Model API:** This API is used to extract data from the receipt image using a vision model.

6. **Receipt OCR Private ECR Repository:** The OCR Lambda function is created from a container stored in this private ECR repository.

7. **Expense Tracker API Container (t2.micro EC2 Instance):** This container runs on an EC2 instance and is responsible for registering users, creating expense records, and uploading receipt images to S3. It also includes monitoring and logging tools such as Prometheus, Grafana, Node Exporter, Traefik, cAdvisor, and goaccess.

8. **AWS RDS PostgreSQL:** The extracted receipt data is stored in a PostgreSQL database running on AWS RDS.

## Workflow
1. A user uploads a receipt image to the S3 bucket.
2. The creation of the object in S3 triggers an event notification.
3. The event notification triggers the Receipt OCR Lambda function.
4. The Lambda function processes the receipt image using the Gemini Vision Model API to extract receipt data.
5. The extracted data is used to create an expense record.
6. The expense record is stored in the PostgreSQL database on AWS RDS.
7. The Expense Tracker API container handles user registration, expense record creation, and uploads receipt images to S3.

## Tech Stack
- **Next.js:** Frontend framework for building the user interface.
- **Python:** Programming language used for backend development.
- **EC2:** Amazon Elastic Compute Cloud for running the Expense Tracker API container.
- **Docker:** Containerization platform for deploying the application components.
- **ECR:** Amazon Elastic Container Registry for storing Docker images.
- **S3:** Amazon Simple Storage Service for storing receipt images.
- **Lambda:** AWS Lambda for serverless processing of receipt images.
- **Gemini:** Vision model API for extracting data from receipt images.
- **GitHub Actions:** CI/CD pipeline for automating the build and deployment process.
- **Grafana:** Monitoring and observability platform.
- **Traefik:** Reverse proxy and load balancer.
- **Prometheus:** Monitoring and alerting toolkit.

## How to Run
1. Clone the repository.
2. Set up the necessary AWS services (S3, Lambda, EC2, RDS, ECR).
3. Build and push the Docker images to the ECR repository.
4. Deploy the application using the provided Docker Compose file.
5. Access the application through the provided endpoint.

## Conclusion
This Expense Tracker API system provides a robust and scalable solution for tracking expenses through receipt images. By leveraging AWS services and Docker containers, the system ensures high availability and performance.
