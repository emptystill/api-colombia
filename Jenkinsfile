pipeline {
  agent any

  tools {
    dotnetsdk 'dotNet'
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
      def scannerHome = tool 'SonarScanner for MSBuild'
      withSonarQubeEnv('SonarQube') {
        sh "dotnet ${scannerHome}/SonarScanner.MSBuild.dll begin /k:\"sqp_1a63050bfeaf1bca1a671691f1ff06eb8e2a5a2b\""
        sh "dotnet ${scannerHome}/SonarScanner.MSBuild.dll end"
      }
    }
  }
}