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
          def scannerHome = tool 'SonarScanner for MSBuild'
          withSonarQubeEnv('SonarQube') {
            sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=sonar-jenkins -Dsonar.sources=api -Dsonar.host.url=http://localhost:9000 -Dsonar.login=sqp_1151a2343674c3c831aeb5f07d1ec70499b0938"
          }
        }
      }
    }
  }
}