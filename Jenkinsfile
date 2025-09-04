pipeline {
    agent any

    tools {
        jdk 'jdk21'  // Make sure this matches Global Tool Configuration
    }

    stages {
        stage('Clone Repository') {
            steps {
                git url: 'https://github.com/yusef-okasha97/Automated-Deployment-Nginx-Pipeline-with-Jenkins.git',
                    branch: 'main',
                    credentialsId: 'GitHub-Token'
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
