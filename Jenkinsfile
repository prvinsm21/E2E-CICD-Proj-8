pipeline {
    agent any
    environment {
        DOCKERHUB_USERNAME = "prvinsm21"
        DOCKERHUB_CREDENTAILS = credentials.(dockerhub)
        DOCKER
    }

    stages {
        stage ('Checkout') {
            steps {
                sh 'echo Passed'
            }
        }

        stage ('Unit testing') {
            steps {
                sh 'mvn test'
            }
        }

        stage ('Integration Test') {
            steps {
                sh 'mvn clean verify -DskipUnittest=true'
            }
        }

        stage ('Build Application') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage ('')
    }
}