pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                // Checkout the source code from GitHub
                git branch: 'main', url: 'https://github.com/your-repo/weather-app.git'
            }
        }
        stage('Install Azure CLI') {
            steps {
                sh 'curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash'
            }
        }
        stage('Login to Azure') {
            steps {
                script {
                    // Use 'az login' to authenticate using your own Azure account
                    sh 'az login --use-device-code'
                }
            }
        }
        stage('Deploy to Azure') {
            steps {
                sh '''
                    az webapp create --name ESISWeatherApp2 --resource-group 1-d05d67e0-playground-sandbox --plan Group7weatherAppServicePlan
                    az webapp deployment source config-zip --resource-group 1-d05d67e0-playground-sandbox --name ESISWeatherApp2 --src weather-app.zip
                    az webapp config appsettings set --resource-group 1-d05d67e0-playground-sandbox --name ESISWeatherApp2 --settings "API_KEY=7d3582ada4896dccd3e42654d40246c4"
                '''
            }
        }
    }
}
