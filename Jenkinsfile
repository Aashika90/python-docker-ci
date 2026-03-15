pipeline {
    agent any

    environment {
        DOCKER_IMAGE_NAME = "my-flask-app"
    }

    stages {
        stage('Clone Repository') {
            steps {
                echo 'Cloning Git repository'
                bat """
                if not exist python-docker-ci (
                    git clone -b main https://github.com/Aashika90/python-docker-ci.git
                )
                """
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image'
                bat """
                cd python-docker-ci
                docker build -t %DOCKER_IMAGE_NAME% .
                """
            }
        }

        stage('Stop Existing Container') {
            steps {
                echo 'Stopping existing Docker container if it exists'
                bat """
                cd python-docker-ci
                docker stop flask-container
                if %ERRORLEVEL% NEQ 0 echo Container not running
                """
            }
        }

        stage('Remove Existing Container') {
            steps {
                echo 'Removing existing Docker container if it exists'
                bat """
                cd python-docker-ci
                docker rm flask-container
                if %ERRORLEVEL% NEQ 0 echo Container not found
                """
            }
        }

        stage('Run Docker Container') {
            steps {
                echo 'Running new Docker container'
                bat """
                cd python-docker-ci
                docker run -d --name flask-container -p 5000:5000 %DOCKER_IMAGE_NAME%
                """
            }
        }
    }
}
