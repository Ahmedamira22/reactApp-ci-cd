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
                git branch: 'main', url: 'https://github.com/Ahmedamira22/reactApp-ci-cd.git'
            }
        }
        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }
        stage('Build React App') {
            steps {
                sh 'npm run build'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image with the specified tag
                    docker.build("$DOCKER_IMAGE")
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    // Use Docker Hub credentials to push the image to Docker Hub
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
            // Clean up workspace after the build
            cleanWs()
        }
    }
}
