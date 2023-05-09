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
  }
}
