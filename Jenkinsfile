// Jenkinsfile for Windows
pipeline {
    agent any

    environment {
        DOCKER_IMAGE_NAME = "my-flask-app" // Replace with your desired image name
    }

    stages {
        stage('Clone Repository') {
            steps {
                echo 'Cloning Git repository'
                // Git works the same on Windows if installed
                bat 'git clone -b main https://github.com/Aashika90/python-docker-ci.git'
                // Move into the repo folder
                bat 'cd python-docker-ci'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image'
                // Windows command to build Docker image
                bat "docker build -t %DOCKER_IMAGE_NAME% ."
            }
        }

        stage('Run Docker Container') {
            steps {
                echo 'Running the Docker container'
                // Stop and remove existing container if exists
                bat "docker stop flask-container || echo Container not running"
                bat "docker rm flask-container || echo Container not found"
                // Run the new container
                bat "docker run -d --name flask-container -p 5000:5000 %DOCKER_IMAGE_NAME%"
            }
        }
    }
}
