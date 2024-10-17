pipeline {
    agent any

    environment {
        AZURE_SUBSCRIPTION = '9734ed68-621d-47ed-babd-269110dbacb1'
        AZURE_RG = '1-8ba3b1fe-playground-sandbox'
        AZURE_APP_NAME = 'Group7weatherApp'
        AZURE_CREDENTIALS = credentials('6017b805-bfc3-4436-bff6-9dc2276627d1')
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/Keran02/weather-app-using-openweathermap-api.git'
            }
        }

        stage('Zip the files') {
            steps {
                sh 'zip -r app.zip Jenkinsfile README.md icons index.html media package-lock.json scripts styles'
            }
        }

        stage('Deploy to Azure App Service') {
            steps {
                script {
                    sh 'az login --service-principal -u "$AZURE_CREDENTIALS_USR" -p "$AZURE_CREDENTIALS_PSW" --tenant "$AZURE_CREDENTIALS_TENANT_ID"'
                    sh 'az webapp deployment source config-zip --resource-group "$AZURE_RG" --name "$AZURE_APP_NAME" --src "app.zip"'
                }
            }
        }
    }
}
