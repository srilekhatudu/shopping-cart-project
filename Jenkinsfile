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
                        // Pointing to the specific path of your Dockerfile
                        sh "docker build -t ${dockerImage}:latest -f src/main/java/com/example/Dockerfile ."
                        
                        sh "echo ${DOCKER_PASS} | docker login -u ${DOCKER_USER} --password-stdin"
                        sh "docker push ${dockerImage}:latest"
                    }
                }
            }
        }

        stage('Deploy to AKS') {
            steps {
                script {
                    // This will look for deployment.yaml in your root folder
                    sh 'kubectl apply -f deployment.yaml'
                }
            }
        }
    }
}
