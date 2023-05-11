pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Build Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', '5b6c696b-8453-45ad-9758-bd2a537f4bd3') {
                        def dockerImage = docker.build("gonchi87/time-app:${env.BUILD_NUMBER}", "-f Dockerfile .")
                        dockerImage.push()
                    }
                }
            }
        }
    }
    
    post {
        success {
            echo 'La imagen Docker se construyó y cargó correctamente en Docker Hub.'
        }
        
        failure {
            echo 'Ocurrió un error durante la construcción o carga de la imagen Docker.'
        }
    }
}

// def dockerImage = docker.build("gonchi87/time-app:${env.BUILD_NUMBER}", "-f Dockerfile .")