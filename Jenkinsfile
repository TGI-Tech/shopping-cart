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
                    // Cloning the repository from GitHub
                    git branch: 'projet', 
                        credentialsId: 'git', 
                        url: 'https://github.com/TGI-Tech/shopping-cart.git'
                }
            }
        }
        stage('Build Sonar Scanner CLI') {
            steps {
                script {
                    // Run Docker build
                    dir("${WORKSPACE}/sonar") {
                        sh "docker build -t tgitech/sonarcli:${BUILD_NUMBER} ."
                    }
                }
            }
        }
        stage('Sonar Scan') {
            steps {
                script {
                    // Run SonarQube scan using the configured environment
                    withSonarQubeEnv('sonar') {
                        sh "docker run --rm tgitech/sonarcli:${BUILD_NUMBER} sonar-scanner"
                    }
                }
            }
        }
    }
}
