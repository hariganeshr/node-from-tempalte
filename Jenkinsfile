pipeline {
    agent any

    environment {
        NODE_ENV = 'production'
        DEPLOY_SERVER = 'your.remote.server'
        DEPLOY_USER = 'deploy_user'
        DEPLOY_PATH = '/var/www/nodeapp'
    }

    stages {
        // stage('Clone Repository') {
        //     steps {
        //         git 'https://github.com/your-org/your-node-app.git'
        //     }
        // }

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'npm test'
            }
        }

        stage('Build') {
            steps {
                // Optional, depending on your app
                sh 'npm run build'
            }
        }

        stage('Deploy') {
            steps {
                // Example with rsync
                sh """
                rsync -avz --delete ./ ${DEPLOY_USER}@${DEPLOY_SERVER}:${DEPLOY_PATH}
                """
            }
        }
    }

    post {
        success {
            echo 'Deployment succeeded!'
        }
        failure {
            echo 'Deployment failed.'
        }
    }
}
