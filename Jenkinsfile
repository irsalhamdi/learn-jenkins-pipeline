pipeline {
    agent any

    environment {
        JAVA_HOME = '/usr/lib/jvm/java-11-openjdk-amd64'
        PATH = "${JAVA_HOME}/bin:${env.PATH}"
        AUTHOR = "irsalhamdi@gmail.com"
    }

    parameters {
        string(name: "NAME", defaultValue: "Guest", description: "What is your name?")
        text(name: "DESCRIPTION", defaultValue: "Guest", description: "Tell me about yourself")
        booleanParam(name: "DEPLOY", defaultValue: false, description: "Need to deploy?")
        choice(name: "SOCIAL_MEDIA", choices: ['Instagram', 'Facebook', 'Twitter'], description: "Which social media are you using?")
        password(name: "SECRET", defaultValue: "", description: "Encrypt Key")
    }

    stages {
        stage('OS Setup'){
            matrix{
                axes{
                    axis{
                        name "OS"
                        values "Linux", "Windows", "Mac"
                    }
                    axis{
                        name "ARC"
                        values "32", "64"
                    }
                }
            }

            stages{
                stage('OS Setup'){
                    steps{
                        echo("Setup ${OS}, ${ARC}")
                    }
                }
            }
        }

        stage('Preparation'){
            stages{
                stage("Prepare Java"){
                    steps{
                        echo("Prepare Java")
                    }
                }
                stage("Prepare Maven"){
                    steps{
                        echo("Prepare Maven")
                    }
                }
            }
        }

        stage('Parameter') {
            steps{
                echo "Hello, ${params.NAME}"
                echo "Your description is, ${params.DESCRIPTION}"
                echo "Your social media is, ${params.SOCIAL_MEDIA}"
                echo "Need to deploy, ${params.DEPLOY}"
                echo "Your secret is, ${params.SECRET}"
            }
        }

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
                sh('echo "App Password : $APP_PSW" > "secret.txt"')
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

            input{
                message "Can we deploy ?"
                ok "Yes, of course"
                submitter "Irsal Hamdi"
                parameters {
                    choice(name: "TARGET_ENV", choices: ['DEV', 'QA', 'PROD'], description: 'Which environment you want to deploy ?')
                }
            }

            steps {
                echo("Deploy to ${TARGET_ENV}")
            }
        }
        stage('Release') {
            when {
                expression {
                    return params.DEPLOY
                }
            }
            steps{
                echo("Release it")
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
