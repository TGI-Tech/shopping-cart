pipeline {
    agent any

    tools {
        sonarQubeScanner 'sonar'
    }

    stages {
        stage('Clean Workspace') {
            steps {
                echo 'Cleaning workspace...'
                deleteDir() // This will clean the workspace
            }
        }
        stage('Clone Repository') {
            steps {
                script {
                    git branch: 'projet', 
                        credentialsId: 'git', 
                        url: 'https://github.com/TGI-Tech/shopping-cart.git'
                }
            }
        }
        stage('Sonar Scan') {
            steps {
                script {
                    withSonarQubeEnv('sonar') {
                        sh "sonar-scanner"
                    }
                }
            }
        }
    }
}
