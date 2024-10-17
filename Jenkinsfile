pipeline {
    agent any

    environment {
        AZURE_SUBSCRIPTION = '9734ed68-621d-47ed-babd-269110dbacb1'  // Azure Subscription ID from your terraform script
        AZURE_RG = '1-8ba3b1fe-playground-sandbox'  // Resource Group
        AZURE_APP_NAME = 'Group7weatherApp'  // Azure Web App name
        AZURE_CREDENTIALS = credentials('6017b805-bfc3-4436-bff6-9dc2276627d1')  // Azure credentials from Jenkins
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/kshitizrohilla/weather-app-using-openweathermap-api.git'
            }
        }

        stage('Deploy to Azure') {
            steps {
                script {
                    // Log in to Azure using service principal credentials
                    sh 'az login --service-principal -u "$AZURE_CREDENTIALS_USR" -p "$AZURE_CREDENTIALS_PSW" --tenant "84f1e4ea-8554-43e1-8709-f0b8589ea118"'  // Tenant ID from terraform script
                    // Deploy the app to Azure App Service using the zip file
                    sh 'az webapp deployment source config-zip --resource-group "$AZURE_RG" --name "$AZURE_APP_NAME" --src "**/*.zip"'
                }
            }
        }
    }
}
