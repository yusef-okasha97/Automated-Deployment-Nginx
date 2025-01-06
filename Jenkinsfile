pipeline {
    agent any

    environment {
        SONARQUBE = 'SonarQube'  // This should match the SonarQube server name in Jenkins configuration
        SONAR_TOKEN = credentials('sonar-token')  // Your SonarQube token stored as a Jenkins secret
    }

    stages {
        stage('Clone Repository') {
            steps {
                git url: 'https://github.com/yusef-okasha97/Automated-Deployment-Nginx-Pipeline-with-Jenkins.git', branch: 'main', credentialsId: 'GitHub-Token'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                script {
                    // Run SonarQube scanner to analyze the code
                    withSonarQubeEnv(SONARQUBE) {
                        sh '''#!/bin/bash
                        sonar-scanner \
                            -Dsonar.projectKey=Nginx \
                            -Dsonar.sources=. \
                            -Dsonar.host.url=http:0.0.0.0:4040 \
                            -Dsonar.login=${SONAR_TOKEN}'''
                    }
                }
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
                    sh 'docker cp index.html nginx:/usr/share/nginx/html/index.html'
                }
            }
        }
    }

    post {
        success {
            sh ' echo succeeded '
        }
        failure {
            sh ' echo failed '
        }
    }
}
