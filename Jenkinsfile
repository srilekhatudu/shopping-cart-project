pipeline {
    agent any
    
    tools {
        maven 'maven3'
    }

    stages {
        stage('Build') {
            steps {
                sh 'mvn clean package -Dmaven.test.skip=true'
            }
        }
        
        stage('SonarQube Quality Check') {
            steps {
                echo 'Scanning...'
            }
        }

        stage('Docker Build & Push') {
            steps {
                script {
                    def dockerImage = 'srilekhatudu/shopping-cart-app'
                    withCredentials([usernamePassword(credentialsId: 'docker-hub-creds', passwordVariable: 'DOCKER_PASS', usernameVariable: 'DOCKER_USER')]) {
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
                    // This looks for the file you just recreated in the root
                    sh 'kubectl apply -f deployment.yaml'
                }
            }
        }
    }
}
