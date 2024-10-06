pipeline {
    agent any

    environment {
        DOCKER_CREDENTIALS_ID = 'Docekr-hub' // Add your Docker Hub credentials ID here
    }

    stages {
        stage('Clone Repository') {
            steps {
                git url: 'https://github.com/yusef-okasha97/Automated-Deployment-Pipeline-with-Jenkins-and-Docker.git', credentialsId: 'GitHub-Token'
            }
        }

        stage('Build Docker Images') {
            steps {
                script {
                    // Build the Docker images defined in your Docker Compose file
                    sh 'docker-compose -f docker-compose.yml build'
                }
            }
        }

 stage('Push to Docker Hub') {
            steps {
                script {
                    // Log in to Docker Hub
                    withDockerRegistry([credentialsId: Docekr-hub]) {
                        sh 'docker-compose -f docker-compose.yml push'
                    }
                }
            }
        }

        stage('Run Docker Compose on Localhost') {
            steps {
                script {
                    // Start the Docker Compose services on localhost
                    sh 'docker-compose -f docker-compose.yml up -d'
                }
            }
        }
    }

    post {
        always {
            // Clean up the Docker environment after the pipeline run
            sh 'docker-compose -f docker-compose.yml down'
        }
    }
}

