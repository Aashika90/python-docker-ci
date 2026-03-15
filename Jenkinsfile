pipeline {
    agent any

    environment {
        IMAGE_NAME = "python-ci-lab"
        CONTAINER_NAME = "python-container"
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/Aashika90/python-docker-ci.git'
            }
        }

        stage('Verify Files') {
            steps {
                // PowerShell equivalent of 'ls -ltr'
                powershell 'Get-ChildItem | Sort-Object LastWriteTime'
            }
        }

        stage('Build Docker Image') {
            steps {
                powershell "docker build -t $env:IMAGE_NAME ."
            }
        }

        stage('Run Container') {
            steps {
                powershell """
                # Remove existing container if it exists
                if (\$(docker ps -a --filter "name=$env:CONTAINER_NAME" -q)) {
                    docker rm -f $env:CONTAINER_NAME
                }
                # Run the container
                docker run -d -p 5000:5000 --name $env:CONTAINER_NAME $env:IMAGE_NAME
                """
            }
        }

        stage('Test Flask App') {
            steps {
                powershell """
                # Wait a few seconds for the container to start
                Start-Sleep -Seconds 5
                # Check if the Flask app responds
                Invoke-WebRequest -Uri http://localhost:5000
                """
            }
        }
    }

    post {
        always {
            powershell "docker ps -a"
            powershell "docker images"
        }
        success {
            echo "Pipeline completed successfully!"
        }
        failure {
            echo "Pipeline failed. Check logs above."
        }
    }
}
