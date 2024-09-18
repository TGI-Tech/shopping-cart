pipeline {
    agent any

    environment {
        SONAR_HOST_URL = 'http://34.207.188.153:9000'
        SONAR_TOKEN = credentials('sonar') // Referencing the token credential
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
                        sh "docker run --rm -e SONAR_HOST_URL=${SONAR_HOST_URL} -e SONAR_TOKEN=${SONAR_TOKEN} tgitech/sonarcli:${BUILD_NUMBER} sonar-scanner -Dsonar.login=${SONAR_TOKEN}"
                    }
                }
            }
        }
    }
}
