pipeline {
  agent any
  
  tools {
    dotnet '7.0.100' // Utilizamos la última versión del SDK de .NET
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
        sh 'dotnet test api.test'
      }
    }
  }
}
