pipeline {
    agent any
    tools {
        maven 'Maven'
    }
    stages {
        stage("Source") {
            steps {
                git branch: 'master', url: 'https://github.com/Fatimaseck9/tp/'
            }
        }
        
         stage("Build") {
            steps {
               
                    script {
                    def workspacePath = env.WORKSPACE
                    bat "cd ${workspacePath} && mvn clean org.jacoco:jacoco-maven-plugin:prepare-agent install"
                }
            }
        }

        stage("SonarQube Analysis") {
            steps {
                
                bat 'mvn sonar:sonar'

                
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
