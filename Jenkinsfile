#!/usr/bin/env groovy
pipeline {
    agent any

    environment {
        GCLOUD_CREDS = credentials('gcloud-creds')
        CLOUDSDK_CORE_PROJECT='in-class-lab1-399521'
        INSTANCE_NAME = 'instance-1'
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
                sh '''
                    gcloud auth activate-service-account --key-file="$GCLOUD_CREDS"
                    gcloud compute scp --zone=${ZONE} your-application.jar ${INSTANCE_NAME}:~/
                    gcloud compute ssh --zone=${ZONE} ${INSTANCE_NAME} --command='sudo systemctl restart your-application'
                '''
            }
        }
    }
}
