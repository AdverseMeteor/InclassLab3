#!/usr/bin/env groovy
pipeline {
    agent any

    environment {
        GOOGLE_APPLICATION_CREDENTIALS = credentials('f6b5221b-7408-44a4-a3a1-88a06fd633f9')
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
