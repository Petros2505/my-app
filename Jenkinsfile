pipeline {
    agent any

    environment {
        DOCKER_CREDENTIALS_ID = 'docker-access-token' // Jenkins credentials ID for Docker Hub
        DOCKER_IMAGE = 'peto2505/my-app'
        // KUBECONFIG = "${GIT_COMMIT}" // Path to kubeconfig in Jenkins
        GIT_HUB_URL = "https://github.com/Petros2505/my-app/tree/main"
    }

    stages {
        stage('Clone Repository') {
            steps {
                // Clone the repository (optional if the Jenkins job already checks out code)
                git url: "${GIT_HUB_URL}"
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    // Use the Docker credentials to log in
                    docker.withRegistry('https://index.docker.io/v1/', DOCKER_CREDENTIALS_ID) {
                        // Build the Docker image
                        sh "docker build -t $DOCKER_IMAGE:$IMAGE_TAG ."
                    }
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    // Login to Docker Hub
                    docker.withRegistry('https://index.docker.io/v1/', DOCKER_CREDENTIALS_ID) {
                        // Push the image
                        sh 'docker push $DOCKER_IMAGE:${GIT_COMMIT}'
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
