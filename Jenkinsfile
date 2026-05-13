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
}
