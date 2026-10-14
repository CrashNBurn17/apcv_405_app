# README APCV 405 Class Project

This repository contains the source code for a sample .NET web application. The project uses Jenkins and Docker to automate the process of building, testing, and deploying the application.



\## Project Description



The purpose of this project is to demonstrate how a Continuous Integration and Continuous Deployment (CI/CD) pipeline works. Jenkins retrieves the application code from GitHub, runs automated tests, builds a Docker image, and pushes that image to Docker Hub. The application is then deployed locally using Docker.



\## Technologies Used



* GitHub for source code management
* Jenkins for CI/CD automation
* .NET for application development
* Docker for containerization
* Docker Hub for image storage
* PowerShell for command-line operations



\## Build Instructions



1. Clone the GitHub repository.
2. Open PowerShell in the project directory.
3. Restore the application dependencies.
4. Build the application.
5. Run the automated tests.



Commands:



```powershell

git clone https://github.com/CrashNBurn17/apcv\_405\_app.git

cd apcv\_405\_app

dotnet restore

dotnet build

dotnet test apcv\_405\_app.sln

```



\## CI/CD Pipeline



The Jenkins pipeline automates the following stages:



1\. Clone Repository - Retrieves the application code from GitHub.

2\. Run Automated Tests - Runs .NET tests to verify the application.

3\. Build Docker Image - Creates a Docker image containing the application.

4\. Push Docker Image - Uploads the image to Docker Hub.

5\. Run Docker Container - Deploys the application locally.

6\. Health Check - Verifies that the deployed application is responding.



The pipeline uses a Jenkinsfile stored in the GitHub repository.



\## Deployment Instructions



The application can be deployed locally using Docker.



First, download the Docker image:



```powershell

docker pull kclemenz/apcv-405-app:latest

```



Next, run the Docker container:



```powershell

docker run -d -p 9090:8080 --name apcv-405-container -e ASPNETCORE\_URLS=http://+:8080 kclemenz/apcv-405-app:latest

```



After deployment, the application can be accessed at:



http://localhost:9090



The application health endpoint is:



http://localhost:9090/health



\## Pipeline Results



The Jenkins pipeline was successfully executed during the project.



The completed pipeline demonstrated that the application could be retrieved from GitHub, tested, packaged into a Docker image, uploaded to Docker Hub, and deployed locally.



\## Conclusion



This project provided hands-on experience with CI/CD automation using Jenkins, GitHub, and Docker. It demonstrated how automated testing and deployment can reduce manual work and help maintain consistency throughout the software development process.

