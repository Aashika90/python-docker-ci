// Jenkinsfile
pipeline {
    agent any // Runs the pipeline on any available Jenkins agent

    environment {
        // Define environment variables
        DOCKER_IMAGE_NAME = "my-flask-app" // Replace with your desired image name
    }

    stages {
        stage('Clone Repository') {
            steps {
                echo 'Cloning Git repository'
                // This step is typically handled automatically when configuring the pipeline in Jenkins
                // to pull from SCM (Source Code Management)
                git url: 'https://github.com/Aashika90/python-docker-ci', branch: 'main'
            }
        }

        stage('Build Docker Image') {
            steps {
                echo 'Building Docker image'
                // Build the Docker image using the Dockerfile in the current directory
                sh "docker build -t ${DOCKER_IMAGE_NAME}:latest ."
            }
        }

        stage('Run Docker Container') {
            steps {
                echo 'Running the Docker container'
                // Stop and remove existing container with the same name for a clean run
                sh "docker stop flask-container || true"
                sh "docker rm flask-container || true"
                // Run the new container in detached mode (-d), mapping port 5000
                sh "docker run -d --name flask-container -p 5000:5000 ${DOCKER_IMAGE_NAME}:latest"
            }
        }
    }
}

