pipeline {
    agent any

    parameters {
        choice(
            name: 'ENVIRONMENT',
            choices: [
                'sandbox',
                'dev',
                'staging',
                'thd',
                'kfi',
                'revoltab',
                'terrakaffe',
                'prod',
                'nonprod',
                'all'
            ],
            description: 'Select Environment'
        )
    }

    environment {
        SOURCE_FOLDER = 'qa-tools/decoders/config-schema/*.json'
        ENV = "${params.ENVIRONMENT}".trim()
    }

    stages {

        stage('Show Selected Environment') {
            steps {
                echo "======================================"
                echo "🚀 User selected ENVIRONMENT = ${ENV}"
                echo "======================================"
            }
        }

        stage('Get latest config files') {
            steps {
                echo 'Get Latest config files'
            }
        }

        /* ================= NON-PROD ================= */

        stage('SANDBOX') {
            when {
                expression { ENV in ['sandbox', 'nonprod', 'all'] }
            }
            steps {
                script {
                    deployToGCP(
                        'afero-sandbox',
                        'general-private-35641fbf-ba72-d3f3-bcee-6bf06d463488',
                        'devices/decoders',
                        SOURCE_FOLDER
                    )
                }
            }
        }

        stage('DEV') {
            when {
                expression { ENV in ['dev', 'nonprod', 'all'] }
            }
            steps {
                script {
                    deployToGCP(
                        'afero-dev',
                        'general-private-6aa2f3c0-54fa-4aed-8028-0f0ad29c1169',
                        'devices/decoders',
                        SOURCE_FOLDER
                    )
                }
            }
        }

        stage('STAGING') {
            when {
                expression { ENV in ['staging', 'nonprod', 'all'] }
            }
            steps {
                script {
                    deployToGCP(
                        'afero-staging',
                        'general-private-9b31109f-a9d6-e6de-cbf5-7d576a4cc100',
                        'devices/decoders',
                        SOURCE_FOLDER
                    )
                }
            }
        }

        /* ================= PROD ================= */

        stage('THD') {
            when {
                expression { ENV in ['thd', 'prod', 'all'] }
            }
            steps {
                script {
                    deployToGCP(
                        'home-depot-production',
                        'general-private-e9372f0d-a271-400a-97cd-fd854dc2e882',
                        'devices/decoders',
                        SOURCE_FOLDER
                    )
                }
            }
        }

        stage('KFI') {
            when {
                expression { ENV in ['kfi', 'prod', 'all'] }
            }
            steps {
                script {
                    deployToGCP(
                        'kingfisher-plc-production',
                        'general-private-392d0237-159f-7b69-497c-a4142184a3fc',
                        'devices/decoders',
                        SOURCE_FOLDER
                    )
                }
            }
        }

        stage('REVOLTAB') {
            when {
                expression { ENV in ['revoltab', 'prod', 'all'] }
            }
            steps {
                script {
                    deployToGCP(
                        'revoltab-production',
                        'general-private-5b210e0f-cf25-3bd8-08aa-c46909c7a4fb',
                        'devices/decoders',
                        SOURCE_FOLDER
                    )
                }
            }
        }

        stage('TERRAKAFFE') {
            when {
                expression { ENV in ['terrakaffe', 'prod', 'all'] }
            }
            steps {
                script {
                    deployToGCP(
                        'terrakaffe-production',
                        'general-private-prod',
                        'devices/decoders',
                        SOURCE_FOLDER
                    )
                }
            }
        }
    }

    post {
        success {
            echo "✅ Pipeline completed successfully for ${ENV}"
        }
        failure {
            echo "❌ Pipeline failed for ${ENV}"
        }
    }
}

/* ================= HELPER FUNCTION ================= */

def deployToGCP(project, bucket, path, sourceFolder) {
    echo "--------------------------------------"
    echo "Deploying to GCP"
    echo "Project : ${project}"
    echo "Bucket  : ${bucket}"
    echo "Path    : ${path}"
    echo "Source  : ${sourceFolder}"
    echo "--------------------------------------"

    // gsutil / gcloud commands go here
}
