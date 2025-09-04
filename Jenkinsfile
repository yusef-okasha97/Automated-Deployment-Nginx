pipeline {
    agent any

    tools {
        jdk 'jdk21'  // Ensure this matches Global Tool Configuration
    }

    stages {
        stage('Clone Repository') {
            steps {
                git url: 'https://github.com/yusef-okasha97/Automated-Deployment-Nginx-Pipeline-with-Jenkins.git',
                    branch: 'main',
                    credentialsId: 'GitHub-Token'
            }
        }

        stage('Build and Run with Docker Compose') {
            steps {
                sh '''
                  echo "Bringing up containers with Docker Compose..."
                  docker-compose -f docker-compose.yml up -d --build
                '''
            }
        }

        stage('Verify Running Containers') {
            steps {
                sh '''
                  echo "Listing running containers..."
                  docker ps
                '''
            }
        }
    }

    post {
        always {
            echo 'Pipeline completed.'
        }
        success {
            echo 'Pipeline completed successfully.'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
