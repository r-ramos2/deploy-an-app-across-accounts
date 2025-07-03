<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Deploy an App Across Accounts

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-compute-ecr)

**Author:** R  

---

![Image](http://learn.nextwork.org/serene_teal_majestic_duck/uploads/aws-compute-ecr_3e91948719)

---

## Introducing Today's Project!

In this special multiplayer project, I'm working with a buddy to learn the fundamentals of AWS by building cloud solutions together, supporting each other, and applying our skills in real-world scenarios through collaboration and hands-on practice.

### What is Amazon ECR?

Amazon ECR is a managed container registry. I used it to push my Docker image, share it with my buddy, and pull their image for collaboration and deployment testing.

### One thing I didn't expect...

I didn’t expect the architecture mismatch error. It was surprising to see how different hardware types can block Docker image pulls without proper multi-platform builds.

### This project took me...

This project took me about 2 hours in total, including setup, troubleshooting, and completing the secret mission tasks with my project buddy.

---

## Creating a Docker Image

I set up a Dockerfile and an index.html file. Both files are needed because the Dockerfile defines how to build the container image using Nginx, and index.html provides the custom web content the container will serve.

My Dockerfile tells Docker to use the latest Nginx image and replace its default web page with my custom index.html, creating a lightweight container that serves my personalized web app when deployed.

### I also set up an ECR repository

ECR stands for Elastic Container Registry. It is important because it securely stores and manages container images in AWS, enabling teams to share consistent, versioned builds for smooth deployments. 

![Image](http://learn.nextwork.org/serene_teal_majestic_duck/uploads/aws-compute-ecr_e7f8g9h0)

---

## Set Up AWS CLI Access

### AWS CLI can let me run ECR commands

AWS CLI is a tool that allows you to interact with AWS services directly from the terminal. The CLI asked for my credentials because it needs specific access keys to authenticate and perform tasks like pushing images to ECR from the terminal.

To enable CLI access, I set up a new IAM user with the permission AmazonEC2ContainerRegistryFullAccess. I also set up an access key for this user, which means I can use these credentials to push images to ECR securely.

To pass my credentials to the AWS CLI, I ran the command aws configure. I had to provide the Access Key ID, Secret Access Key, and the AWS region (e.g., us-west-2) to complete the setup.

![Image](http://learn.nextwork.org/serene_teal_majestic_duck/uploads/aws-compute-ecr_4aa3e4fe6)

---

## Pushing My Image to ECR

Push commands are a set of commands that allow you to interact with your Amazon ECR repository. They help push your Docker images into ECR and authenticate Docker with your repository.

### There are three main push commands

To authenticate Docker with my ECR repo, I used the command aws ecr get-login-password --region <region> | docker login --username AWS --password-stdin <aws_account_id>.dkr.ecr.<region>.amazonaws.com.

To push my container image, I ran the command `docker push <repository-uri>:latest`. Pushing means uploading my local Docker image to ECR, making it available for others to pull and deploy from the cloud.

When I built my image, I tagged it with the label latest. This means that the image is the most current version, and any deployment referencing latest will always pull the most up-to-date container image.

---

## Resolving Permission Issues

When I tried pulling my project buddy's container image for the first time, I saw the error 403 Forbidden. This was because our private repositories block access without proper cross-account permissions.

To resolve each other's permission errors, my buddy and I updated our ECR repository policy by inserting our ARNs and granting pull permissions (ecr:BatchCheckLayerAvailability, ecr:BatchGetImage, ecr:GetDownloadUrlForLayer).

![Image](http://learn.nextwork.org/serene_teal_majestic_duck/uploads/aws-compute-ecr_74b90da414)

---

## Deploying the App

---

## Resolving Deployment Issues

---

---
