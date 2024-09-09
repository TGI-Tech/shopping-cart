pipeline {
    agent any

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
                        credentialsId: 'Git-hub-credential', 
                        url: 'https://github.com/TGI-Tech/shopping-cart.git'
                }
            }
        }
    }
}
