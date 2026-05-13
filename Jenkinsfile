pipeline {
    agent any
    
    tools {
        maven 'maven3'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building the Shopping Cart App...'
                sh 'mvn clean package'
            }
        }
    }
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
        
        // --- ADD THESE STAGES BELOW ---
        stage('SonarQube Quality Check') {
            steps {
                echo 'Scanning code for vulnerabilities...'
                // We will add the Sonar scanner command here next
            }
        }

       stage('Docker Build & Push') {
            steps {
                script {
                    def dockerImage = 'srilekhatudu/shopping-cart-app'
                    
                    withCredentials([usernamePassword(credentialsId: 'docker-hub-creds', passwordVariable: 'DOCKER_PASS', usernameVariable: 'DOCKER_USER')]) {
                        // Builds the image using your Dockerfile
                        sh "docker build -t ${dockerImage}:latest ."
                        
                        // Logs into your Docker Hub and pushes the image
                        sh "echo ${DOCKER_PASS} | docker login -u ${DOCKER_USER} --password-stdin"
                        sh "docker push ${dockerImage}:latest"
                    }
                }
            }
        }
        // ------------------------------
    }
}
