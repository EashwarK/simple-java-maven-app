pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Starting Build stage'
                sh 'mvn -B -DskipTests clean package'
                echo 'Build stage completed'
            }
        }
        stage('Test') {
            steps {
                echo 'Starting Test stage'
                sh 'mvn test'
                echo 'Test stage completed'
            }
            post {
                always {
                    echo 'Publishing JUnit test results'
                    junit 'target/surefire-reports/*.xml'
                    echo 'JUnit test results published'
                }
            }
        }
        stage('Deliver') {
            steps {
                echo 'Starting Deliver stage'
                sh './jenkins/scripts/deliver.sh'
                echo 'Deliver stage completed'
            }
        }
    }
    post {
        failure {
            echo 'Pipeline failed'
        }
    }
}
