pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
 repositry
                git url:'https://github.com/yusef-okasha97/Automated-Deployment-Pipeline-with-Jenkins-and-Docker.git',branch:'main'
            }
        }

        stage('Run Docker Compose on Localhost') {
            steps {
                script {
                    // Start the Docker Compose services on localhost
                    sh 'echo "pipeline done"'
                }
            }
        }
    } // Close the stages block
} // Close the pipeline block


