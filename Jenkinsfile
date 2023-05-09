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
        stage('Test') {
            steps {
                bat "dotnet test"
            }
        }
        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    bat "dotnet sonarscanner begin /k:\"sonar-jenkins\" /d:sonar.host.url=\"http://localhost:9000\" /d:sonar.login=\"sqp_1151a2343674c3c831aeb5f07d1ec70499b0938c\""
                    bat "dotnet build"
                    bat "dotnet sonarscanner end /d:sonar.login=\"sqp_1151a2343674c3c831aeb5f07d1ec70499b0938c\""
                }
            }
        }
    }
}
