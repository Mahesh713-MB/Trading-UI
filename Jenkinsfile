pipeline {
    agent any

    environment {
        NODE_OPTIONS = '--openssl-legacy-provider'
    }
    
    stages {
        stage('Git Checkout') {
            steps {
                git 'https://github.com/Mahesh713-MB/Trading-UI.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'npm install --legacy-peer-deps'
            }
        }

        stage('NPM Audit') {
            steps {
                sh 'npm audit || true'
            }
        }

        stage('Build') {
            steps {
                sh 'npm run build'
            }
        }

        stage('Deploy with PM2') {
            steps {
                sh '''
                    pm2 delete Trading-UI || true
                    pm2 serve build 3000 --name Trading-UI --spa
                    pm2 save
                '''
            }
        }
    }
}
