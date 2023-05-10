pipeline {
  agent any

  tools {
    dotnetsdk 'dotNet' // Utilizamos la última versión del SDK de .NET
    msbuild 'SonarScanner for MSBuild'
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
          sh './sonar-scanner-4.6.2.2472/bin/sonar-scanner -Dsonar.login="sqp_1a63050bfeaf1bca1a671691f1ff06eb8e2a5a2b" -Dsonar.projectKey="sonar-jenkins"'
        }
      }
    }
  }
}