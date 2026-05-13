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
                echo 'Creating Docker Image...'
                // This is where we containerize the app
            }
        }
        // ------------------------------
    }
}
