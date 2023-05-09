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
    stage('SonarQube Analysis') {
      steps {
        script {
          scannerHome = tool 'SonarScanner for MSBuild'
        }
        withSonarQubeEnv('SonarQube analysis') {
          sh "dotnet ${scannerHome}/SonarScanner.MSBuild.dll begin /k:\"sonar-jenkins\""
          sh "dotnet build"
          sh "dotnet ${scannerHome}/SonarScanner.MSBuild.dll end"
        }
      }
    }
  }
}