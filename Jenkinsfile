pipeline {
  agent any

  tools {
    dotnetsdk 'dotNet' // Utilizamos la última versión del SDK de .NET
  }

  stages {
    stage('Restore') {
      steps {
        sh 'dotnet restore api'
      }
    }

    stage('Build') {
      steps {
        sh 'dotnet build api'
      }
    }

    stage('Análisis de código con SonarScanner') {
      steps {
        withSonarQubeEnv('SonarQube') {
          sh 'wget https://github.com/SonarSource/sonar-scanner-msbuild/releases/download/5.2.1.31210/sonar-scanner-msbuild-5.2.1.31210-netcoreapp3.0.zip'
          sh 'unzip sonar-scanner-msbuild-5.2.1.31210-netcoreapp3.0.zip'
          sh './sonar-scanner-4.6.2.2472/bin/sonar-scanner -Dsonar.login="sqp_1a63050bfeaf1bca1a671691f1ff06eb8e2a5a2b" -Dsonar.projectKey="sonar-jenkins"'
        }
      }
    }
  }
}