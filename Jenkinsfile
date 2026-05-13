pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building the Shopping Cart App...'
                sh 'mvn clean package'
            }
        }
    }
}

