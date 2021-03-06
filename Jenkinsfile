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
        stage('Checkout') {
          steps {
            echo "Checking Out BPM Delete Codebase"
            echo "======================================================="
            checkout scm
            echo "======================================================="
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
                    echo "======================================================="
                    echo "report"
                    echo "======================================================="
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Deliver') {
            steps {
                echo 'DELIVER AAAAAAAAAAAAAAA'
                sh 'pwd'
                sh 'ls'
                sh './jenkins/scripts/deliver.sh'
            }
        }
    }
    post {
        always {
            echo 'This will always run'
        }
        success {
            echo 'This will run only if successful'
        }
        failure {
            echo 'This will run only if failed'
        }
        unstable {
            echo 'This will run only if the run was marked as unstable'
        }
        changed {
            echo 'This will run only if the state of the Pipeline has changed'
            echo 'For example, if the Pipeline was previously failing but is now successful'
        }
    }
}
