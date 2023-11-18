#!/usr/bin/env groovy
pipeline {
    agent any

    environment {
        GOOGLE_APPLICATION_CREDENTIALS = credentials('in-class-lab1-399521')
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout source code from version control
                checkout scm
            }
        }
        stage('Build') {
            steps {
                echo 'Building..'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Deploy') {
            steps {
                script {
                    
                    // Use gcloud commands with the provided credentials
                    sh "gcloud auth activate-service-account --key-file=${GOOGLE_APPLICATION_CREDENTIALS}"
                    sh "gcloud compute deploy ..."
                }
            }
        }
    }
}
