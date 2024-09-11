pipeline {
    agent any

    tools {
        // Define the SonarQube scanner tool to use (adjust the name if needed)
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
                    // Cloning the repository from GitHub
                    git branch: 'projet', 
                        credentialsId: 'git', 
                        url: 'https://github.com/TGI-Tech/shopping-cart.git'
                }
            }
        }
        stage('Sonar Scan') {
            steps {
                script {
                    // Run SonarQube scan using the configured environment
                    withSonarQubeEnv('sonar') {
                        // SonarQube scanner will use sonar-project.properties in the project root
                        sh "sonar-scanner"
                    }
                }
            }
        }
    }
}
