pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Hello Build 1'
                sleep(5)
                echo 'Hello Build 2'
                echo 'Hello Build 3'
            }
        }
        stage('Test') {
            steps {
                echo 'Hello Test 1'
                sleep(5)
                echo 'Hello Test 2'
                echo 'Hello Test 3'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Hello Deploy 1'
                sleep(5)
                echo 'Hello Deploy 2'
                echo 'Hello Deploy 3'
            }
        }
    }

    post {
        always{
            echo "Always Running !"
        }
        success {
            echo "Only running while success"
        }
        failure {
            echo "Only running when failure"
        }
        cleanup{
            echo "Only running while finish the pipeline"
        }
    }
}
