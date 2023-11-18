#!/usr/bin/env groovy
pipeline {
    agent any

    environment {
        GCLOUD_CREDS = credentials('gcloud-creds')
        CLOUDSDK_CORE_PROJECT='in-class-lab1-399521'
        INSTANCE_NAME = 'instance-2'
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
                    gcloud config set project ${CLOUDSDK_CORE_PROJECT}
                    gcloud config set compute/zone ${ZONE}
                    
                    gcloud compute instances create ${INSTANCE_NAME} --image-family=debian-10 --image-project=debian-cloud --tags=http-server

                    gcloud compute ssh ${INSTANCE_NAME} --command='sudo mkdir -p /var/www/html/'
                    gcloud compute scp --recurse Hello.html ${INSTANCE_NAME}:/var/www/html/
                    gcloud compute ssh ${INSTANCE_NAME} --command='sudo apt-get update && sudo apt-get install -y apache2 && sudo service apache2 start'
                '''
            }
        }
    }
}
