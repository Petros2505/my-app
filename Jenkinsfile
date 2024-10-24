pipeline {
    agent any

    environment {
        DOCKER_CREDENTIALS_ID = 'docker-access-token' // Jenkins credentials ID for Docker Hub
        DOCKER_IMAGE = 'my-app'
        // KUBECONFIG = "${GIT_COMMIT}" // Path to kubeconfig in Jenkins
        GIT_HUB_URL = "https://github.com/Petros2505/my-app.git"
    }

    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    docker.build("${DOCKER_IMAGE}:${GIT_COMMIT}")
                }
            }
        }
        stage('Push to Docker Hub') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', DOCKER_CREDENTIALS) {
                        docker.image("${IMAGE_NAME}:${GIT_COMMIT}").push()
                    }
                }
            }
            }

    //     stage('Deploy to Minikube') {
    //         steps {
    //             script {
    //                 // Set up the Kubeconfig (if necessary)
    //                 sh 'export KUBECONFIG=$KUBECONFIG'

    //                 // Apply Kubernetes deployment
    //                 sh '''
    //                     kubectl apply -f deployment.yaml
    //                 '''
    //             }
    //         }
    //     }
    // }

    // post {
    //     always {
    //         // Clean up resources if needed
    //         cleanWs()
    //     }
    }
}
}
