pipeline {
    agent any
    tools {
        maven 'Maven'
    }
    environment{
        SONAR_URL="http://10.0.0.241:9000"
    }
    stages {
        stage("Source") {
            steps {
                git branch: 'main', url: 'https://github.com/tonux/tp-master-sir-2023.git'
            }
        }
        stage("Build") {
            steps {
                sh 'mvn clean org.jacoco:jacoco-maven-plugin:prepare-agent install'
            }
        }
        stage("SonarQube Analysis") {
            steps {
                sh 'mvn sonar:sonar -Dsonar.host.url=$SONAR_URL'
            }
        }
        stage('Approve Deployment') {
            input {
                message "Do you want to proceed for deployment?"
            }
            steps {
                sh 'echo "Deploying into Server"'
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