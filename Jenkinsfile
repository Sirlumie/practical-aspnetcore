pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out branch net8.0...'
                // Use Git to explicitly checkout the 'net8.0' branch
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: '*/net8.0']],
                    userRemoteConfigs: [[url: 'https://github.com/Sirlumie/practical-aspnetcore.git']],
                    extensions: [[$class: 'CloneOption', depth: 1, noTags: true, shallow: true]]
                ])

            }
        }

        stage('Restore Dependencies') {
            steps {
                echo 'Restoring dependencies...'
                // Ensure to restore using the correct solution file
                sh 'dotnet restore projects/net9/open-api-3.sln'
            }
        }

        stage('Build') {
            steps {
                echo 'Building the project...'
                // Build the solution file
                sh 'dotnet build projects/net9/open-api-3.sln --configuration Release --no-restore'
            }
        }
    }

    post {
        success {
            echo 'Build succeeded!'
        }
        failure {
            echo 'Pipeline failed. Check logs for errors.'
        }
    }
}
