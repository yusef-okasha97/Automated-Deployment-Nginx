pipeline {
    agent any  // Specify the agent label for VM2

    stages {
        stage('Clone Repository') {
            steps {
                git url: 'https://github.com/yusef-okasha97/Automated-Deployment-Pipeline-with-Jenkins.git', branch: 'main', credentialsId: 'GitHub-Token'
            }
        }

        stage('Build Docker Images') {
            steps {
                script {
                    sh 'docker-compose -f docker-compose.yml build'
                }
            }
        }

        stage('Run Docker Compose on Localhost') {
            steps {
                script {
                    sh 'docker-compose -f docker-compose.yml up -d'
                }
            }
        }

        stage('Copy index.html to Nginx Container') {
            steps {
                script {
                    // Replace 'nginx' with your actual container name
                    sh 'docker cp index.html  nginx_nginx_1:/usr/share/nginx/html/index.html'
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished.'
        }
    }
}

