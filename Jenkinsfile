pipeline {
    agent any
    stages {
        stage('Hello') {
            steps {
                echo 'My Jenkins Pipeline'
            }
        }
        stage('Checkout') {
            steps {
                echo 'Melakukan checkout dari SCM...'
                checkout scm
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    echo 'Membangun Docker image...'
                    docker.build("${IMAGE_NAME}:${env.BUILD_NUMBER}")
                    echo "Image berhasil dibuat: ${IMAGE_NAME}:${env.BUILD_NUMBER}"
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    echo 'Push image ke Docker Hub...'
                    docker.withRegistry(REGISTRY, REGISTRY_CREDENTIALS) {
                        docker.image("${IMAGE_NAME}:${env.BUILD_NUMBER}").push()
                        docker.image("${IMAGE_NAME}:${env.BUILD_NUMBER}").push('latest')
                    }
                }
            }
        }
    }
    post {
        always {
            echo 'Selesai build 🏁OYYY'
        }
    }
}
