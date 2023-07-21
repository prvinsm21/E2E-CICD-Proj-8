pipeline {
    agent any
    environment {
        DOCKERHUB_USERNAME = "prvinsm21"
        DOCKERHUB_CREDENTIALS = credentials('dockerhub')
        DOCKERIMAGE_NAME = "prvinsm21/photo-site:${BUILD_NUMBER}"
    }

    stages {
        stage ('Git Checkout') {
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

        stage ('Static Code Analysis') {
            steps {
                script {
                    withSonarQubeEnv(credentialsId: 'sonar-api') {
                    sh 'mvn clean package sonar:sonar'
                    }
                }
            }
        }

        stage ('Quality gate status') {
            steps {
                script {
                    waitForQualityGate abortPipeline: false, credentialsId: 'sonar-api'
                }
            }
        }

        
    }
}