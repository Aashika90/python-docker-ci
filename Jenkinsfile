pipeline {
    agent any 

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/discover-devops/python-docker-ci.git'
            }
        }

        stage('Verify Files') {
            steps {
                // Windows equivalent of 'ls -ltr'
                bat 'dir'
            }
        }

        stage('Build Docker Image') {
            steps {
                bat 'docker build -t python-ci-lab .'
            }
        }

        stage('Run Container') {
            steps {
                bat '''
                REM Remove existing container if it exists
                for /f %%i in ('docker ps -a -q --filter "name=python-container"') do docker rm -f %%i
                REM Run the container
                docker run -d -p 5000:5000 --name python-container python-ci-lab
                '''
            }
        }

    }
}
