pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Start Build'
                sh('./mvnw clean compile test')
                echo('Finish Build')
            }
        }
        stage('Test') {
            steps {
                echo 'Start Build'
                sh('./mvnw test')
                echo('Finish Build')
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
