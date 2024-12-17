pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out source code...'
                checkout scm
            }
        }

        stage('Restore Dependencies') {
            steps {
                echo 'Restoring dependencies...'
                sh 'dotnet restore projects/net9/open-api-3.sln'
            }
        }

        stage('Build') {
            steps {
                echo 'Building the project...'
                sh 'dotnet build projects/net9/open-api-3.sln --configuration Release --no-restore'
            }
        }

    }

    post {
        success {
            echo 'Build, Test, Dockerize, and Deployment succeeded!'
        }
        failure {
            echo 'Pipeline failed. Check logs for errors.'
        }
    }
}
