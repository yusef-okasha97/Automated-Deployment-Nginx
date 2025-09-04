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
