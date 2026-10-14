pipeline {
    agent any

    environment {
        IMAGE_NAME = 'kclemenz/apcv-405-app'
        CONTAINER_NAME = 'apcv-405-container'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/CrashNBurn17/apcv_405_app.git'
            }
        }

        stage('Run Automated Tests') {
            steps {
                bat 'dotnet test apcv_405_app.sln'
            }
        }

        stage('Build Docker Image') {
    	    steps {
        	bat '''
            	@echo off
            	set "PATH=C:\\Users\\adrum\\AppData\\Local\\Programs\\DockerDesktop\\resources\\bin;%PATH%"
            	docker --version
            	docker build -t %IMAGE_NAME%:latest .
            '''
    	    }
	}

	stage('Push Docker Image') {
    	    steps {
       	 	withCredentials([usernamePassword(
            	credentialsId: 'dockerhub-credentials',
            	usernameVariable: 'DOCKER_USER',
            	passwordVariable: 'DOCKER_TOKEN'
        	)]) {
            	bat '''
               	@echo off
                echo %DOCKER_TOKEN% | docker login -u %DOCKER_USER% --password-stdin
                docker push %IMAGE_NAME%:latest
            '''
            }
    	}
    }

        stage('Run Docker Container') {
            steps {
                bat '''
                    docker rm -f %CONTAINER_NAME% 2>NUL
                    docker run -d -p 9090:8080 --name %CONTAINER_NAME% -e ASPNETCORE_URLS=http://+:8080 %IMAGE_NAME%:latest
                '''
            }
        }

        stage('Health Check') {
            steps {
                bat 'powershell -Command "Start-Sleep -Seconds 10; $response = Invoke-RestMethod http://localhost:9090/health; if ($response -ne \'Healthy\') { exit 1 }"'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }

        failure {
            echo 'Pipeline failed. Check the console output.'
        }
    }
}