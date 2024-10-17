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

        stage('Deploy to Azure') {
            steps {
                azureWebAppPublish azureCredentialsId: '6017b805-bfc3-4436-bff6-9dc2276627d1', 
                                   resourceGroup: '1-8ba3b1fe-playground-sandbox', 
                                   appName: 'Group7weatherApp', 
                                   filePath: '**/*' // Deploys all files (HTML, JS, etc.)
            }
        }
    }
}
