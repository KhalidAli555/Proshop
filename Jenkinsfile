pipeline {
    agent any

    environment {
        FRONTEND_IMAGE = "khalidali07/frontend-app:${env.BRANCH_NAME}-${env.BUILD_NUMBER}"
        BACKEND_IMAGE  = "khalidali07/backend-app:${env.BRANCH_NAME}-${env.BUILD_NUMBER}"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: "main", url: 'https://github.com/KhalidAli555/Proshop.git'
            }
        }

        stage('Build Docker Images') {
            steps {
                sh "docker build -t $FRONTEND_IMAGE ./frontend"
                sh "docker build -t $BACKEND_IMAGE ./backend"
            }
        }

        stage('Login to Docker Hub') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-login', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh 'echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin'
                }
            }
        }

        stage('Push Docker Images') {
            steps {
                sh "docker push $FRONTEND_IMAGE"
                sh "docker push $BACKEND_IMAGE"
            }
        }
    }

    post {
        always {
            echo "✅ Pipeline completed"
        }
        cleanup {
            sh 'docker logout'
        }
    }
}
