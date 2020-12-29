pipeline {
    agent any
    environment {
        //variable for image name
        PROJECT = "pipeline-demo"
    }
    stages {
        stage('Initialize') {
            steps {
                deleteDir()
            }
        }
        stage('Clean Workspace') {
            steps {
                checkout scm
            }
        }
        stage ('Build and Push') {
            steps {
                            withCredentials([[$class: 'UsernamePasswordMultiBinding', 
                            credentialsId: 'dockerhub-cred',
                            usernameVariable: 'REGISTRY_USER', 
                            passwordVariable: 'REGISTRY_PASSWORD']]) {
                        sh 'docker build -t ${REGISTRY_USER}/${PROJECT} .'
                        sh 'docker login -u ${REGISTRY_USER} -p ${REGISTRY_PASSWORD} '
                        sh 'docker push ${REGISTRY_USER}/${PROJECT}'
                    }
                }
        }
        }
    }
