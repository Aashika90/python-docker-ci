pipeline {

    agent any 
    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/Aashika90/python-docker-ci.git'
            }
        }

        stage('Verify Files') {
            steps {
                sh 'ls -ltr'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t python-ci-lab .'
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                docker rm -f python-container || true
                docker run -d -p 5000:5000 --name python-container python-ci-lab
                '''
            }
        }

    }
}
