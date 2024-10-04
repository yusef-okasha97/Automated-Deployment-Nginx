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

        stage('Run Tests') {
            steps {
                script {
                    // Start services in detached mode
            sh 'docker-compose -f docker-compose.yml up -d'

            // Wait for services to start (optional, based on your application)
            sleep 15 // Adjust the duration based on your application’s startup time

            // Run your tests
            sh './run_tests.sh' // A script to run tests, adjust accordingly

            // Stop services after tests
            sh 'docker-compose -f docker-compose.yml down'
                }
            }
        }

        stage('Push to Docker Hub') {
            steps {
                script {
                    // Log in to Docker Hub
                    withDockerRegistry([credentialsId: DOCKER_CREDENTIALS_ID]) {
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

