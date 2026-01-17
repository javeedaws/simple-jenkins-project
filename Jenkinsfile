pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
                echo "Cloning source code"
                checkout scm
            }
        }

        stage('Verify Files') {
            steps {
                echo "Checking workspace content"
                sh '''
                pwd
                ls -l
                '''
            }
        }

        stage('Deploy to Apache') {
            steps {
                echo "Deploying index.html"
                sh '''
                sudo cp index.html /var/www/html/index.html
                sudo systemctl restart httpd
                '''
            }
        }
    }

    post {
        success {
            echo "Deployment successful"
        }
        failure {
            echo "Deployment failed"
        }
    }
}
