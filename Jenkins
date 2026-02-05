pipeline {
    agent any

    parameters {
        choice(
            name: 'ENVIRONMENT',
            choices: ['sandbox','dev','staging','thd','kfi','revoltab','terrakaffe','prod','nonprod','all'],
            description: 'Select Environment'
        )
    }

    environment {
        SOURCE_FOLDER = 'qa-tools/decoders/config-schema/*.json'
    }

    stages {

        stage('Get latest config files') {
            steps {
                echo 'Get Latest config files'
            }
        }

        stage('SANDBOX') {
            when {
                expression { params.ENVIRONMENT in ['sandbox','nonprod','all'] }
            }
            steps {
                script {
                    def GCP_PROJECT = 'sandbox'
                    def GCP_BUCKET = 'general-private-35641fbf-ba72'
                    def GCP_BUCKET_PATH = 'devices/decoders'

                    deployToGCP(GCP_PROJECT, GCP_BUCKET, GCP_BUCKET_PATH, env.SOURCE_FOLDER)
                }
            }
        }

        stage('DEV') {
            when {
                expression { params.ENVIRONMENT in ['dev','nonprod','all'] }
            }
            steps {
                script {
                    def GCP_PROJECT = 'dev'
                    def GCP_BUCKET = 'general-private-6aa2f3c0'
                    def GCP_BUCKET_PATH = 'devices/decoders'

                    deployToGCP(GCP_PROJECT, GCP_BUCKET, GCP_BUCKET_PATH, env.SOURCE_FOLDER)
                }
            }
        }

        stage('STAGING') {
            when {
                expression { params.ENVIRONMENT in ['staging','nonprod','all'] }
            }
            steps {
                script {
                    def GCP_PROJECT = 'staging'
                    def GCP_BUCKET = 'general-private-9b31109f'
                    def GCP_BUCKET_PATH = 'devices/decoders'

                    deployToGCP(GCP_PROJECT, GCP_BUCKET, GCP_BUCKET_PATH, env.SOURCE_FOLDER)
                }
            }
        }

        stage('THD') {
            when {
                expression { params.ENVIRONMENT in ['thd','prod','all'] }
            }
            steps {
                script {
                    def GCP_PROJECT = 'home-production'
                    def GCP_BUCKET = 'general-private-e9372f0d'
                    def GCP_BUCKET_PATH = 'devices/decoders'

                    deployToGCP(GCP_PROJECT, GCP_BUCKET, GCP_BUCKET_PATH, env.SOURCE_FOLDER)
                }
            }
        }
    }

    post {
        success {
            echo "✅ Pipeline completed successfully for ${params.ENVIRONMENT}"
        }
        failure {
            echo "❌ Pipeline failed"
        }
    }
}

def deployToGCP(project, bucket, path, sourceFolder) {
    echo "Deploying to GCP"
    echo "Project: ${project}"
    echo "Bucket: ${bucket}"
    echo "Path: ${path}"
    echo "Source folder: ${sourceFolder}"
}
