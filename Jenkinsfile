pipeline {
    agent any

    environment {
        JAVA_HOME = '/usr/lib/jvm/java-11-openjdk-amd64'
        PATH = "${JAVA_HOME}/bin:${env.PATH}"
        AUTHOR = "irsalhamdi@gmail.com"
    }

    stages {
        stage('Prepare'){

            environment{
                APP = credentials("irsal_hamdi_secret")
            }

            steps{
                echo("Start Job : ${env.JOB_NAME}")
                echo("Author : ${AUTHOR}")
                echo("Start Build : ${env.BUILD_NUMBER}")
                echo("Branch Name : ${env.BRANCH_NAME}")
                echo("APP USER : ${APP_USR}")
                echo("APP_PASSWORD : ${APP_PSW}")
                echo('echo "App Password : $APP_PSW" > "secret.txt"')
            }
        }
        stage('Build') {

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
