pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                git url: 'https://github.com/yusef-okasha97/Automated-Deployment-Nginx-Pipeline-with-Jenkins.git', branch: 'main', credentialsId: 'GitHub-Token'
            }
        }

        stage('Build Docker Images') {
            steps {
                script {
                    sh 'docker-compose -f docker-compose.yml build'
                }
            }
        }

        stage('Run SonarQube Analysis (Optional)') {
            steps {
                // Replace with your actual credentials IDs or use environment variables
                withCredentials([usernamePassword(credentialsId: 'sonar-token', usernameVariable: 'SONAR_TOKEN', passwordVariable: 'SONAR_TOKEN')]) {
                    sh '''
                        sonar-scanner \
                          -Dsonar.projectKey="Nginx" \
                          -Dsonar.sources="src/main/index.html" \  # Adjust the path to your source code if needed
                          -Dsonar.host.url="http://0.0.0.0:4040" \
                          -Dsonar.login="${SONAR_TOKEN}"
                    '''
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
                    sh 'docker cp index.html  nginx:/usr/share/nginx/html/index.html'
                }
            }
        }
    }

    post {
        success {
            slackSend(channel: 'nginx', message: "Build ${env.BUILD_NUMBER} succeeded!")
        }
        failure {
            slackSend(channel: 'nginx', message: "Build ${env.BUILD_NUMBER} failed!")
        }
    }
}
