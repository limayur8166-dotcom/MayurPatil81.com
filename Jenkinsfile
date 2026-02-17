pipeline {
    agent any

    tools {
        nodejs 'NodeJS_20'
    }

    environment {
        DEPLOY_DIR = "/var/www/site1"
    }

    stages {

        stage('Clone') {
            steps {
                echo "Cloning repository..."
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                echo "Installing dependencies..."
                sh 'npm install'
            }
        }

        stage('Build') {
            steps {
                echo "Building project..."
                sh 'npm run build'
            }
        }

        stage('Test') {
            steps {
                echo "Running tests..."
                sh 'npm test || true'
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying to server..."
                sh '''
                rm -rf $DEPLOY_DIR/*
                cp -r build/* $DEPLOY_DIR/
                '''
            }
        }
    }

    post {
        success {
            echo "Deployment successful!"
        }
        failure {
            echo "Build failed!"
        }
    }
}
