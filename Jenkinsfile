pipeline {
    agent any

    environment {
        AZURE_RG = '1-8ba3b1fe-playground-sandbox'
        AZURE_APP_NAME = 'Group7weatherApp'
    }

    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/Keran02/weather-app-using-openweathermap-api.git'
            }
        }

        stage('Zip the files') {
            steps {
                script {
                    // Zip the files in the current workspace
                    sh 'zip -r app.zip *'
                }
            }
        }

        stage('Deploy to Azure') {
            steps {
                script {
                    // Using Azure CLI to log in with the provided credentials and deploy the app
                    sh '''
                        az login --service-principal -u "a2a53fb5-c734-4d48-833d-474a60773103" -p "IIN8Q~xkeP4~NkavvnGppqkbncSF0KEjOKOWvasZ" --tenant "84f1e4ea-8554-43e1-8709-f0b8589ea118"
                        az webapp deployment source config-zip --resource-group "$AZURE_RG" --name "$AZURE_APP_NAME" --src "app.zip"
                    '''
                }
            }
        }
    }
}
