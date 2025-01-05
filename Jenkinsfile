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
                    sh 'docker cp index.html  nginx:/usr/share/nginx/html/index.html'
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
        stage('SonarQube Analysis') {
          def scannerHome = tool 'SonarScanner';
          withSonarQubeEnv() {
          sh "${scannerHome}/bin/sonar-scanner"
    }

}

