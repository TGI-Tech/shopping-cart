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
        stage('Build Sonar Scanner CLI') {
            steps {
                script {
                    // Run SonarQube scan using the configured environment
                    Dir('${WORKSPACE}/sonar') {
                        // SonarQube scanner will use sonar-project.properties in the project root
                        sh "docker build -t tgitech/sonarcli:v1 ."
                    }
                }
            }
            }
        }
        stage('Sonar Scan') {
            steps {
                script {
                    // Run SonarQube scan using the configured environment
                    withSonarQubeEnv('sonar') {
                        docker.image('tgitech/sonarcli:v1').inside{
                        sh "sonar-scanner"
                    }
                }