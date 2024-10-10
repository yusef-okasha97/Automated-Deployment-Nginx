pipeline {
    agent any

    environment {
        DOCKER_HUB_CREDENTIALS = credentials('Docker-token') // Replace with your Jenkins credentials ID
        IMAGE_NAME = 'yusef_ok97@yahoo.com/wordpress' // Replace with your Docker Hub username and desired image name
    }

    stages {
        stage('Clone Repository') {
            steps {
                git url: 'https://github.com/yusef-okasha97/Automated-Deployment-Pipeline-with-Jenkins-and-Docker.git', branch: 'main', credentialsId: 'GitHub-Token'
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

        stage('Push Docker Image to Docker Hub') {
            steps {
                script {
                    // Log in to Docker Hub
                    sh "echo ${DOCKER_HUB_CREDENTIALS.password} | docker login -u ${DOCKER_HUB_CREDENTIALS.username} --password-stdin"
                    
                    // Tag the image (if needed)
                    sh "docker tag your-local-image-name:latest ${IMAGE_NAME}:latest" // Replace with your local image name

                    // Push the image to Docker Hub
                    sh "docker push ${IMAGE_NAME}:latest"
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
