pipeline {
  agent any
  
  tools {
    dotnet '7.0.5' // Utilizamos la última versión del SDK de .NET
  }
  
  stages {   
    stage('Restore') {
      steps {
        sh 'dotnetRestore api'
      }
    }
    
    stage('Build') {
      steps {
        sh 'dotnetBuild api'
      }
    }
    
    stage('Test') {
      steps {
        sh 'dotnetTest api.test'
      }
    }
  }
}
