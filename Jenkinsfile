pipeline {
  agent any

  environment {
    ASPNETCORE_ENVIRONMENT = 'Production'
    DOTNET_CLI_TELEMETRY_OPTOUT = '1'
  }

  stages {
    stage('Checkout') {
      steps {
        // Checkout source code from Git
        checkout scm
      }
    }

    stage('Build and Publish') {
      steps {
        // Build and publish the ASP.NET Core application
        script {
          sh 'dotnet restore'
          sh 'dotnet build --configuration Release'
          sh 'dotnet publish --configuration Release --output bin/publish'
        }
      }
    }

    stage('Deploy to Azure Web App') {
      steps {
        // Deploy to Azure Web App using Azure App Service Deploy plugin
        script {
          azureWebAppPublish appName: 'sam1256app.azurewebsites.net',
                              resourceGroup: 'sam1256app_group',
                              filePath: 'bin/publish',
                              publishType: 'filePath',
                              targetDirectory: '/site/wwwroot'
        }
      }
    }
  }
}
