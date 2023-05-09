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

    stage('install-sonarscanner') {
      steps {
        sh 'dotnet tool install dotnet-sonarscanner --add-source "https://api.nuget.org/v3/index.json" --ignore-failed-sources'
      }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    sh "dotnet sonarscanner begin /k:\"sonar-jenkins\" /d:sonar.host.url=\"http://localhost:9000\" /d:sonar.login=\"sqp_1151a2343674c3c831aeb5f07d1ec70499b0938c\""
                    sh "dotnet build"
                    sh "dotnet sonarscanner end /d:sonar.login=\"sqp_1151a2343674c3c831aeb5f07d1ec70499b0938c\""
                }
            }
        }
    }
}
