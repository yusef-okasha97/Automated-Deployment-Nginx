pipeline {
    agent any

    tools {
        jdk 'jdk21'  // Use the JDK 17 tool configured in Jenkins' Global Tool Configuration
    }

        // Stage to clone the Git repository
        stage('Clone Repository') {
            steps {
                git url: 'https://github.com/yusef-okasha97/Automated-Deployment-Nginx-Pipeline-with-Jenkins.git', branch: 'main', credentialsId: 'GitHub-Token'
            }
        }

        // Stage for SonarQube Analysis
        stage('SonarQube Analysis') {
            steps {
                script {
                    // Run SonarQube scanner to analyze the code
                    withSonarQubeEnv(SONARQUBE) {
                        sh '''#!/bin/bash
                        sonar-scanner \
                            -Dsonar.projectKey=Nginx \
                            -Dsonar.sources=. \
                            -Dsonar.host.url=http://172.17.0.5:9000 \
                            -Dsonar.login=${SONAR_TOKEN} || { echo 'SonarQube analysis failed'; exit 1; }
                        '''
                    }
                }
            }
        }

        // Additional stages can go here, e.g., Build, Test, Deploy

    }

    post {
        always {
            // Clean up or any necessary post-build steps, if needed
            echo 'Pipeline completed.'
        }
        success {
            // Actions on successful pipeline completion
            echo 'Pipeline completed successfully.'
        }
        failure {
            // Actions in case of failure (could include notification, etc.)
            echo 'Pipeline failed.'
        }
    }
}
