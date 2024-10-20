pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                // Checkout the source code from GitHub
                git branch: 'main', url: 'https://github.com/Keran02/weather-app-using-openweathermap-api.git', credentialsId: 'githubpat'
            }
        }
         stage('Zip the files') {
            steps {
                sh 'zip -r app.zip icons index.html media scripts styles'
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
        stage('Create Azure Web App') {
            steps {
                // Create the Azure web app with Node.js runtime (adjust if necessary)
                sh '''
                    az webapp create --name ESISWeatherApp3 --resource-group 1-dfbc852d-playground-sandbox --plan Group7weatherAppServicePlan --runtime "node|16-lts"
                '''
            }
        }
        stage('Deploy to Azure') {
            steps {
                // Deploy the app using a zip package
                sh '''
                    az webapp deployment source config-zip --resource-group 1-dfbc852d-playground-sandbox --name ESISWeatherApp3 --src app.zip
                    az webapp config appsettings set --resource-group 1-dfbc852d-playground-sandbox --name ESISWeatherApp3 --settings "API_KEY=7d3582ada4896dccd3e42654d40246c4"
                '''
            }
        }
    }
}
