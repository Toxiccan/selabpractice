is it triggered after error

This is to show that the webhook is triggered


pipeline {
    agent any

    tools {
        maven 'MAVEN_HOME'
    }

    stages {

        stage('Git Clone') {
            steps {
                bat """
                    rmdir /S /Q selabpractice 2>nul
                    git clone https://github.com/Toxiccan/selabpractice.git
                """
            }
        }

        stage('Clean') {
            steps {
                bat "mvn clean -f selabpractice"
            }
        }

        stage('Install') {
            steps {
                bat "mvn install -f selabpractice"
            }
        }

        stage('Test') {
            steps {
                bat "mvn test -f selabpractice"
            }
        }

        stage('Package') {
            steps {
                bat "mvn package -f selabpractice"
            }
        }
    }
}
