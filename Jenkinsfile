pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                echo 'Pulling latest code from GitHub...'
                git branch: 'main', url: 'https://github.com/<username>/jenkins-web-app.git'
            }
        }

        stage('Deploy to Web Server') {
            steps {
                echo 'Deploying application to Apache web root...'
                sh '''
                    rm -rf /var/www/html/*
                    cp -r * /var/www/html/
                '''
            }
        }

        stage('Verify Deployment') {
            steps {
                echo 'Verifying HTTP response...'
                sh 'curl -I http://localhost'
            }
        }
    }

    post {
        success {
            echo 'Deployment completed successfully!'
        }
        failure {
            echo 'Deployment failed. Check the console logs.'
        }
    }
}
