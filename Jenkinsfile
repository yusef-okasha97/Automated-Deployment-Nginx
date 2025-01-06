pipeline {
    agent any

    environment {
        JAVA_HOME = '/usr/lib/jvm/java-17-openjdk-amd64'  // Adjust this path if needed based on your system
        PATH = "${JAVA_HOME}/bin:${env.PATH}"  // Ensure Java 17 is used in the PATH
        SONARQUBE = 'SonarQubeServer'  // Your SonarQube server configuration
        SONAR_TOKEN = credentials('sonar-token')  // SonarQube token
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
                            -Dsonar.host.url=http://172.17.0.2:9000 \
                            -Dsonar.login=${SONAR_TOKEN}'''
                    }
                }
            }
        }

        // Other pipeline stages...
    }
}
