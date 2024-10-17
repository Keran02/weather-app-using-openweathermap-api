pipeline {
    agent any

    environment {
        AZURE_CREDENTIALS = 'azure-credentials'
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/kshitizrohilla/weather-app-using-openweathermap-api.git'
            }
        }

        stage('Deploy to Azure') {
            steps {
                azureWebAppPublish azureCredentialsId: 'azure-credentials', 
                                   resourceGroup: '1-8ba3b1fe-playground-sandbox', 
                                   appName: 'Group7weatherApp', 
                                   filePath: '**/*' // Deploys all files (HTML, JS, etc.)
            }
        }
    }
}
