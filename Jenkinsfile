pipeline {
  environment {
    gitUrl = "https://github.com/powerPlant/qiime2-srf.git"
    gitCredential = "github_powerPlant"
    gitBranch = "master"
    appRecipe = "Apptainer"
    appImage = "qiime2"
    appVersion = "2023.5"
 }

agent { label 'apptainer' }

stages {
    stage('Clone git') {
        steps {
            git branch: gitBranch, changelog: false, credentialsId: gitCredential, poll: false, url: gitUrl
        }
    }
    
    stage('Build') {
      steps {
        sh "sudo apptainer build ${appImage}-${appVersion}.sif ${appRecipe}.${appVersion}"
      }
    }

    stage('Copy') {
      steps {
        sh "cp ${appImage}-${appVersion}.sif /workspace/output"
      }
    }
}
}
