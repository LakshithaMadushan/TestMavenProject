def COLOR_MAP = [
    'SUCCESS': 'good', 
    'FAILURE': 'danger',
]

def getBuildUser() {
    return currentBuild.rawBuild.getCause(Cause.UserIdCause).getUserId()
}

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
        stage('Slack it'){
            steps {
                slackSend channel: '#jenkins-build-test-slack', 
                          message: 'Hello, this is jenkins pipeline msg from BUDDY'
            }
        }
    }
    
    // Post-build actions
    post {
        always {
            script {
                BUILD_USER = getBuildUser()
            }
            echo 'I will always say hello in the console.'
            slackSend channel: '#jenkins-build-test-slack',
                color: COLOR_MAP[currentBuild.currentResult],
                message: "*${currentBuild.currentResult}:* Job ${env.JOB_NAME} build ${env.BUILD_NUMBER} by ${BUILD_USER}\n More info at: ${env.BUILD_URL}"
        }
    }
}
