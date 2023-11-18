#!/usr/bin/env groovy
pipeline {
    agent any

    environment {
        GOOGLE_APPLICATION_CREDENTIALS = credentials('6cd6dbf7-848f-437d-ad68-2baa3ea1d548')
        PROJECT_ID = 'in-class-lab1-399521'
        INSTANCE_NAME = 'Application'
        ZONE = 'us-central1-a'
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
                    
                    // Deploy the application to Google Compute Engine
                    sh "gcloud compute scp --zone=${ZONE} your-application.jar ${INSTANCE_NAME}:~/"
                    sh "gcloud compute ssh --zone=${ZONE} ${INSTANCE_NAME} --command='sudo systemctl restart your-application'"
                    
                    sh "gcloud compute deploy ..."
                }
            }
        }
    }
}
