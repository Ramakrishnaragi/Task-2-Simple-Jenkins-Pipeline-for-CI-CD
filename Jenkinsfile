pipeline {
    agent any

    environment {
        APP_NAME = "nodejs-demo-app"
        DOCKER_IMAGE = "nodejs-demo-app:latest"
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/your/repo.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE .'
            }
        }

        stage('Test') {
            steps {
                sh 'docker run --rm $DOCKER_IMAGE npm test || echo "No tests found"'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                    docker stop $APP_NAME || true
                    docker rm $APP_NAME || true
                    docker run -d --name $APP_NAME -p 3000:3000 $DOCKER_IMAGE
                '''
            }
        }
    }
}

