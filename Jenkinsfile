pipeline {
    agent {
        docker {
            image 'maven:3-alpine'
            args '-v /root/.m2:/root/.m2'
        }
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
                echo 'TEST '
                sh 'pwd'
                sh 'ls'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Deliver') {
            steps {
                echo 'DELIVER QQQQQQQQQQQQQQ'
                sh 'pwd'
                sh 'ls'
                sh './jenkins/scripts/deliver.sh'
            }
        }
    }
}
