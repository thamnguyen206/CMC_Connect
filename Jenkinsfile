pipeline {
    agent any
    tools {
        maven 'Maven 3.8.6'
        jdk 'JDK17'
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
                sh 'git log -1 --oneline'
            }
        }
        stage('Build') {
            steps {
                dir('backend') {
                    sh 'mvn -B clean compile'
                }
            }
        }
        stage('Test') {
            steps {
                dir('backend') {
                    sh 'mvn -B test'
                }
            }
        }
    }
    post {
        always {
            junit allowEmptyResults: true, testResults: 'backend/target/surefire-reports/*.xml'
        }
        success {
            echo 'Pipeline thanh cong'
        }
        failure {
            echo 'Pipeline that bai, xem Console Output de biet nguyen nhan'
        }
    }
}
