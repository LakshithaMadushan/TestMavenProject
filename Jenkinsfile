pipeline {
    agent any 
    tools {
        maven 'Maven 3.6.3'
    }
    stages {
        stage('--Clean--') { 
            steps {
                sh "mvn clean"
            }
        }
        stage('--Test--') { 
            steps {
                sh "mvn test" 
            }
        }
        stage('--Deploy--') { 
            steps {
                sh "mvn package"
            }
        }
    }
}
