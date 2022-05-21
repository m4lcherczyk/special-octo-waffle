#!/usr/bin/env groovy

pipeline {
    agent { dockerfile true }
    environment {
        registry = "mmalcherczyk/jenkins-docker-test"
        registryCredential = 'dockerhub'
        dockerImage = ''

    }
    stages {
        stage('Clone repository') {
            steps {
                git 'https://github.com/m4lcherczyk/special-octo-waffle.git'
            }
        }

        stage('Build image') {
            steps {
                script{
                    app = docker.build registry
                }
            }
        }

        stage('Test') {
            steps {
                echo 'OK!'
            }
        }
        stage('Deploy') {
            steps {
                script{
                    docker.withRegistry( '', registryCredential ) {
                        app.withRegistry("${env.BUILD_NUMBER}")
                        app.push()
                    }
                }
            }
        }
    }
}
