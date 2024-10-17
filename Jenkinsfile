pipeline {
    agent any

    environment {
        AZURE_CREDENTIALS = 'azure-credentials'
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/Keran02/weather-app-using-openweathermap-api.git'
            }
        }

        stage('Build') {
            steps {
                sh 'npm install' // Use npm install if you need to build anything
            }
        }

        stage('Deploy to Azure') {
            steps {
                azureWebAppPublish azureCredentialsId: 'azure-credentials', 
                                   resourceGroup: '1-8ba3b1fe-playground-sandbox', 
                                   appName: 'Group7weatherApp', 
                                   filePath: '**/*.zip'
            }
        }
    }
}
