# CI/CD Pipeline with GitHub Actions for EKS Deployment

## Project Overview

In this project, I developed a comprehensive CI/CD pipeline using GitHub Actions to automate the deployment of a containerized Python application to an existing Amazon EKS cluster. The pipeline handles the complete workflow from code commit to production deployment, including Docker image building, ECR repository management, and Kubernetes deployment orchestration.

## Implementation Process

### CI/CD Pipeline Development with GitHub Actions

Working with an existing EKS cluster, I focused on building a robust CI/CD pipeline using GitHub Actions. This involved creating a workflow that would automatically build, push, and deploy Docker images to the EKS cluster whenever changes were pushed to the repository.

The workflow was designed to be comprehensive yet maintainable, with clearly defined steps and proper error handling. I structured the GitHub Actions workflow file to execute the following steps on each push to the master branch:

1. **Environment Preparation**: Configures the runner with necessary tools and credentials
2. **Docker Image Building**: Compiles the application into a Docker image with the commit hash as tag
3. **ECR Authentication and Pushing**: Securely authenticates with ECR and pushes the tagged image
    
4. **Kubernetes Deployment**: Updates the EKS cluster with the new image version using kubectl

### Authentication Challenges and Solutions

One of the most significant challenges I faced was implementing secure authentication between GitHub Actions and AWS services. Initially, I attempted to use static AWS credentials stored as GitHub Secrets, but this approach presented security concerns and maintenance overhead.

To address these issues, I implemented OpenID Connect (OIDC) authentication between GitHub Actions and AWS. This modern approach eliminated the need for storing long-lived credentials by allowing GitHub Actions to assume an IAM role directly. The implementation required:

1. Configuring an OIDC identity provider in AWS IAM that trusts GitHub's OIDC provider
2. Creating an IAM role with appropriate permissions and a trust policy that validates GitHub's OIDC claims
3. Updating the GitHub Actions workflow to use the `configure-aws-credentials` action with OIDC authentication

This solution significantly enhanced security by implementing short-lived credentials and reducing the risk of credential exposure.

### Kubernetes Manifest Development

I created Kubernetes manifests for deploying the application to EKS, focusing on best practices for production deployments. The manifests included:

1. **Deployment configuration**: Defining container specifications, resource limits, health checks, and update strategies
2. **Service definition**: Exposing the application with appropriate networking settings
3. **ConfigMap and Secret management**: Handling configuration and sensitive data securely

A key challenge was implementing dynamic image references in the manifests. I solved this by using a template approach with placeholders that are replaced during the deployment process:

---

### Troubleshooting and Resolving Pipeline Issues

Throughout the development process, I encountered and resolved numerous pipeline issues, as evidenced by the GitHub Issues I closed:

1. **Authentication Issues**: Resolved problems with AWS credential configuration by implementing OIDC authentication and ensuring proper IAM role permissions.
2. **Action Resolution Errors**: Fixed issues with GitHub Actions not finding required actions by correctly referencing the action paths and ensuring proper syntax in the workflow file.
3. **ECR Push Failures**: Addressed Docker build and push failures by debugging registry authentication issues and optimizing the Docker build process.
4. **EKS Deployment Errors**: Solved problems with applying changes to the EKS cluster by ensuring proper kubeconfig setup and troubleshooting permission issues.
5. **Manifest Application Failures**: Fixed issues with Kubernetes manifests not being properly applied by implementing better error handling and validation in the deployment step.

Each issue required careful analysis of logs and error messages, followed by targeted solutions that addressed the root cause rather than just the symptoms.

## Technical Implementation Details

The GitHub Actions workflow I developed demonstrates several DevOps best practices:

---

A key learning experience was understanding how GitHub Actions work, particularly:

1. **Action Composition**: Learning how to combine pre-built actions with custom scripts
2. **Context and Expression Syntax**: Mastering GitHub's expression syntax for accessing outputs and variables
3. **Workflow Optimization**: Implementing strategies to reduce build times and improve reliability

## Results and Benefits

The implemented CI/CD pipeline delivered significant improvements:

1. **Deployment Automation**: Eliminated manual deployment steps, reducing human error and saving time
2. **Enhanced Security**: Implemented OIDC authentication for secure, short-lived credentials
3. **Improved Traceability**: Each deployment is linked to a specific commit, enhancing auditability
4. **Developer Experience**: Simplified the deployment process to a single git push
5. **Faster Feedback**: Developers receive immediate feedback on deployment success or failure

## Conclusion

This project demonstrates my ability to implement modern DevOps practices and overcome complex technical challenges. By developing a robust CI/CD pipeline with GitHub Actions, I created a reliable, secure, and efficient workflow for deploying applications to Amazon EKS.

The systematic approach to troubleshooting and resolving issues showcases my problem-solving skills and persistence in the face of technical obstacles. Each resolved issue contributed to my understanding of the technologies involved and helped create a more resilient pipeline.

The skills developed during this project—including GitHub Actions configuration, Kubernetes manifest management, and AWS service integration—have prepared me for tackling more complex DevOps challenges in the future.
