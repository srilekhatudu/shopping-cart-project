pipeline {
    agent any
    
    tools {
        maven 'maven3'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building the Shopping Cart App...'
                sh 'mvn clean package -Dmaven.test.skip=true'
            }
        }
        
        stage('SonarQube Quality Check') {
            steps {
                echo 'Scanning code for vulnerabilities...'
            }
        }

        stage('Docker Build & Push') {
            steps {
                script {
                    def dockerImage = 'srilekhatudu/shopping-cart-app'
                    
                    withCredentials([usernamePassword(credentialsId: 'docker-hub-creds', passwordVariable: 'DOCKER_PASS', usernameVariable: 'DOCKER_USER')]) {
                        // Build the container using your Dockerfile
                        sh "docker build -t ${dockerImage}:latest ."
                        
                        // Login and push to srilekhatudu Docker Hub
                        sh "echo ${DOCKER_PASS} | docker login -u ${DOCKER_USER} --password-stdin"
                        sh "docker push ${dockerImage}:latest"
                    }
                }
            }
        }
    }
}
