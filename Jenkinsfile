pipeline {
    agent any

    triggers {
        // Triggers the pipeline automatically when a change is pushed to GitHub
        githubPush() 
    }

    environment {
        // Ensures tools like npm know they are running in a CI environment
        CI = 'true'
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from the Git repository
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                // Using npm install (if you use npm ci it requires a package-lock.json in sync)
                // If your jenkins server is strictly on windows, change 'sh' to 'bat'
                sh 'npm install'
            }
        }

        stage('Lint') {
            steps {
                sh 'npm run lint'
            }
        }

        stage('Build') {
            steps {
                sh 'npm run build'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t react-todo-app .'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed. Please check the build logs.'
        }
    }
}
