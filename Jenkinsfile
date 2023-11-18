#!/usr/bin/env groovy
pipeline {
    agent any

    environment {
        GCLOUD_CREDS = credentials('gcloud-creds')
        CLOUDSDK_CORE_PROJECT='in-class-lab1-399521'
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
                sh '''
                    gcloud auth activate-service-account --key-file="$GCLOUD_CREDS"
                    gcloud compute zones list
                '''
            }
        }
        stage('Deploy') {
            steps {
                script {

                    echo 'Deploying..'
                    
                    
                    // Deploy the application to Google Compute Engine
                    //sh "gcloud compute scp --zone=${ZONE} your-application.jar ${INSTANCE_NAME}:~/"
                    //sh "gcloud compute ssh --zone=${ZONE} ${INSTANCE_NAME} --command='sudo systemctl restart your-application'"
                    
                }
            }
        }
    }
}
