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
            // Send success email
            mail to: 'javeedaws60@gmail.com',
                 subject: "Jenkins Job '${env.JOB_NAME}' Successful",
                 body: "Good news! The Jenkins job '${env.JOB_NAME}' (${env.BUILD_NUMBER}) succeeded.\nCheck console output at: ${env.BUILD_URL}"
        }
        failure {
            echo "Deployment failed"
            // Send failure email
            mail to: 'javeedaws60@gmail.com',
                 subject: "Jenkins Job '${env.JOB_NAME}' Failed",
                 body: "Alert! The Jenkins job '${env.JOB_NAME}' (${env.BUILD_NUMBER}) failed.\nCheck console output at: ${env.BUILD_URL}"
        }
    }
}
