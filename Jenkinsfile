def projectName = "mi-proyecto"
def scannerKey = "sqp_1a63050bfeaf1bca1a671691f1ff06eb8e2a5a2b"

pipeline {
  agent any

  tools {
    dotnetsdk 'dotNet'
    // Agregue una herramienta para SonarScanner
    sonarqube 'SonarScanner for MSBuild'
  }

  stages {
    stage('Restore') {
      steps {
        sh "dotnet restore ${projectName}"
      }
    }

    stage('Build') {
      steps {
        sh "dotnet build ${projectName}"
      }
    }

    stage('SonarQube Analysis') {
      steps {
        script {
          withSonarQubeEnv('SonarQube') {
            // Agregue la tarea de compilación antes de analizar el código
            sh "dotnet build ${projectName}"
            sh "dotnet ${tool 'SonarScanner for MSBuild'}/SonarScanner.MSBuild.dll begin /k:\"${scannerKey}\""
            sh "dotnet ${tool 'SonarScanner for MSBuild'}/SonarScanner.MSBuild.dll end"
          }
        }
      }
    }

    // Agregue una etapa adicional para la implementación de la aplicación
    stage('Deployment') {
      steps {
        sh 'echo "Implementando la aplicación..."'
        // Agregue aquí los comandos de implementación
      }
    }
  }
}