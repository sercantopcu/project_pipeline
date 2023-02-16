# Project Pipeline
## This project uses a continuous delivery pipeline to automate the deployment of the Spring PetClinic web application to a Google Cloud Platform (GCP) environment.
Prerequisites
Before setting up the pipeline, you'll need to have the following prerequisites:
* A GitHub account
* A GCP account
* The gcloud command-line tool installed and configured with your GCP credentials
* Docker installed on your local machine
* Access to the SonarQube service, if you plan to use it for code quality analysis
Setting up the Pipeline
To set up the pipeline for this project, follow these steps:
1. Fork the project repository to your own GitHub account.
2. Enable the following APIs:
    * Google Container Registry API
    * Cloud Build API
    * Google Cloud Storage JSON API
3. Create a new service account with the following IAM roles:
    * Service Account User ( basic owner )
4. Generate a new key for the service account and download it as a JSON file.
5. Add the following repository secrets to your GitHub repository:
    * PROJECT_ID: The ID of your GCP project 
    * GOOGLE_DOMAIN_NAME: Your domain name.
    * SERVICE_ACCOUNT: The JSON key file for the service account created in step 3.
6. Copy the contents of the pipeline.yml file in this repository to a new file in your project repository named .github/workflows/pipeline.yml.
7. Modify the values of the environment variables in the pipeline.yml file to match your project setup:
    * repo: The URL of your project repository
    * app_version: The version of the application to deploy (e.g., main)
    * repo_region: The GCP region where you want to deploy your application (e.g., us-central1)
    * project_id: The ID of your GCP project (same as the PROJECT_ID repository secret)
    * app_name: The name of your application (e.g., spring-petclinic-now)
    * tag_new_version: A unique tag for the new version of the application (e.g., ${GITHUB_SHA})
    * enable_sonar: Whether to use SonarQube for code quality analysis (e.g., true or false)
    * sonar_organization: The organization ID for your SonarQube instance
    * sonar_projectKey: The project key for your SonarQube instance
    * sonar_login: The authentication token for your SonarQube instance
# Using the Pipeline
## Once you have set up the pipeline, you can use it to deploy new versions of web application to your GCP environment.
## To trigger the pipeline, simply push changes to the main branch of your project repository. The pipeline will automatically build a new Docker image of the application, tag it with a unique version number, and push it to the Google Container Registry in your GCP project. The pipeline will then deploy the new image to a Project Infrastructure cluster, making it publicly accessible at the service URL.
## If you have enabled SonarQube in the pipeline, the pipeline will also perform a code quality analysis of the application and display the results in your SonarQube instance.