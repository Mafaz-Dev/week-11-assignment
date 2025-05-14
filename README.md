# Week-11 Assignment: MERN Stack Blog App Deployment

## Description

In this assignment, I focused on deploying a MERN stack blog application using AWS services, Terraform, and Ansible. The goal was to set up a scalable architecture that included a backend running on an EC2 instance, a frontend hosted on S3, and a MongoDB Atlas database.

## Steps Taken

### 1. Designing the Architecture

I started by sketching out the architecture for the application. The design included an EC2 instance for the backend, MongoDB Atlas for the database, and S3 buckets for both the frontend and media uploads. This helped me visualize how the components would interact.

### 2. Security Configuration

Next, I created an IAM policy and user for programmatic access to the S3 bucket designated for media uploads. I also set up a security group for the EC2 instance to allow SSH, HTTP, and the application’s port (5000). This ensured that my application was secure while still accessible.

### 3. Setting Up MongoDB Atlas

I created a free-tier cluster on MongoDB Atlas and whitelisted the IP address of my EC2 instance. After creating a user for the database, I obtained the connection string, which would be crucial for my backend configuration.

### 4. Configuring S3 Buckets

I set up two S3 buckets: one for the frontend and another for media uploads. I enabled static website hosting for the frontend bucket and added a bucket policy to allow public read access. For the media bucket, I allowed programmatic access and applied a CORS policy to facilitate media uploads.

### 5. Launching the Backend with Terraform

I created a launch template using Terraform to provision my EC2 instance. I chose a t3.micro instance running Ubuntu 22.04 and configured it to allow SSH connections with my existing key pair.

### 6. Automating Backend Server Setup with Ansible

To streamline the backend setup, I wrote an Ansible playbook. This playbook automated the provisioning of the backend server by:

- Cloning the blog application repository from GitHub.
- Generating and configuring the `.env` file with MongoDB and S3 credentials.
- Starting the backend application using PM2.

I ensured that the playbook was idempotent and structured it according to best practices, using variables for sensitive data.

### 7. Deploying the Frontend

For the frontend, I created another Ansible playbook. This playbook navigated to the frontend directory, created a `.env` file with the necessary configurations, and set up AWS CLI with the IAM credentials I had created earlier. After installing dependencies and building the frontend, I deployed it to the S3 bucket.

### 8. Testing the Application

After deployment, I tested the entire application to ensure everything was functioning as expected. I verified that the frontend loaded correctly from S3, the backend was running smoothly on EC2, and media uploads worked seamlessly.

### 9. Cleanup

Once I confirmed that the application was fully operational, I used Terraform to destroy all AWS resources created during the assignment. I also removed any sensitive credentials from the EC2 instance and deleted any manually created MongoDB Atlas users.

## Conclusion

This assignment was a valuable experience in deploying a full-stack application using cloud services. I learned how to effectively use Terraform and Ansible for infrastructure as code, and I gained a deeper understanding of AWS services and their configurations.
