pipeline {
    agent any
    tools {
        maven 'Maven'
    }
     environment{
        SONAR_URL="http:// 192.168.1.9:9000"
    }

    stages {
        stage("Source") {
            steps {
                git branch: 'master', url: 'https://github.com/Fatimaseck9/tp/'
            }
        }
        
         stage("Build") {
            steps {
               
                  bat 'mvn clean org.jacoco:jacoco-maven-plugin:prepare-agent install'

            }
        }

        stage("SonarQube Analysis") {
            steps {
                
                bat 'mvn sonar:sonar-Dsonar.host.url=$SONAR_URL'


                
            }
        }
        stage('Approve Deployment') {
            input {
                message "Do you want to proceed for deployment?"
            }
            steps {
                bat 'echo "Deploying into Server"'
            }
        }
    }
    post {
        aborted {
            echo "Sending message to agent"
        }
        failure {
            echo "Sending message to agent"
        }
        success {
            echo "Sending message to agent"
        }
    }
}
