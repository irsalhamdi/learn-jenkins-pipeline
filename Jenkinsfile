pipeline {
    agent none

    environment {
            JAVA_HOME = '/usr/lib/jvm/java-11-openjdk-amd64'
            PATH = "${JAVA_HOME}/bin:${env.PATH}"
    }

    stages {
        stage('Build') {
            agent {
                node {
                    label 'built-in'
                }
            }

            steps {

                script{
                    for(int i=0; i < 10; i++){
                        echo("${i}")
                    }
                }

                echo 'Start Build'
                sh('./mvnw clean compile test')
                echo('Finish Build')
            }
        }
        stage('Test') {
            agent {
                node{
                    label 'built-in'
                }
            }

            steps {

                script{
                    def data = [
                        "firstName": "Irsal",
                        "lastName": "Hamdi"
                    ]
                    writeJSON(file: "data.json", json:data)
                }

                echo 'Start Build'
                sh('./mvnw test')
                echo('Finish Build')
            }
        }
        stage('Deploy') {
            agent {
                node {
                    label 'built-in'
                }
            }

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
