pipeline {
    agent {
        docker { image 'node:18' }
    }
    environment {
        DOCKER_IMAGE = 'ahmedamira22/react-app:latest'
    }
    stages {
        stage('Checkout Code') {
            steps {
                echo "Checking out code from Git"
                git branch: 'main', url: 'https://github.com/Ahmedamira22/reactApp-ci-cd.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                echo "Installing dependencies"
                sh 'npm install'
            }
        }
        stage('Build React App') {
            steps {
                echo "Building React App"
                sh 'npm run build'
            }
        }
        stage('Build Docker Image') {
            steps {
                echo "Building Docker image"
                script {
                    docker.build("$DOCKER_IMAGE")
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                echo "Pushing Docker image to Docker Hub"
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'docker-hub-credentials') {
                        docker.image("$DOCKER_IMAGE").push()
                    }
                }
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploy step can be added here'
            }
        }
    }
    post {
        always {
            echo 'Cleaning workspace'
            cleanWs()
        }
    }
}
