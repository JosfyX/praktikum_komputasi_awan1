pipeline {
    agent any
    environment {
        IMAGE_NAME = 'abdieeuh/simple-app'
        REGISTRY = 'https://index.docker.io/v1/'
        REGISTRY_CREDENTIALS = 'dockerhub-credentials'
        DOCKER_HOST = "unix:///var/run/docker.sock"
    }
    stages {
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
                    // Aktifkan kembali saat kredensial Docker Hub sudah siap
                    /*
                    docker.withRegistry(REGISTRY, REGISTRY_CREDENTIALS) {
                        docker.image("${IMAGE_NAME}:${env.BUILD_NUMBER}").push()
                        docker.image("${IMAGE_NAME}:${env.BUILD_NUMBER}").push('latest')
                    }
                    */
                    echo 'Tahap Push dilewati (testing lokal).'
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
