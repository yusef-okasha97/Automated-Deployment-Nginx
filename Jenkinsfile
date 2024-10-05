pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git url: 'https://github.com/yusef-okasha97/Automated-Deployment-Pipeline-with-Jenkins-and-Docker.git', credentialsId: 'GitHub-Token'
            }
        }

    
        stage('Run Docker Compose on Localhost') {
            steps {
                script {
                    // Start the Docker Compose services on localhost
                    sh 'docker-compose -f docker-compose.yml up -d'
                    sh 'echo "pipline done "'
                }
            }
        }
    }


