pipeline {
    agent any

    parameters {
        choice(
            name: 'ENVIRONMENT',
            choices: ['PR01', 'PR02'],
            description: 'Select Environment'
        )

        choice(
            name: 'SERVICE_TYPE',
            choices: [
                'Service user',
                'Permission',
                'Submission',
                'B1 core',
                'F1 core'
            ],
            description: 'Select Service Type'
        )
    }

    stages {

        stage('Password Verification') {
            steps {
                script {

                    def inputData = input(
                        message: "Enter password to continue",
                        parameters: [
                            password(name: 'PIPELINE_PASSWORD', description: 'Enter password')
                        ]
                    )

                    def userPassword = inputData['PIPELINE_PASSWORD']

                    def storedPass

                    withCredentials([string(credentialsId: 'pipeline-run-password', variable: 'STORED_PASS')]) {
                        storedPass = STORED_PASS
                    }

                    if (userPassword.trim() == storedPass.trim()) {
                        echo "✅ Password validation successful"
                    } else {
                        error("❌ Invalid password")
                    }

                }
            }
        }
        
        stage('Print Selection') {
            steps {
                echo "Environment Selected: ${params.ENVIRONMENT}"
                echo "Service Selected: ${params.SERVICE_TYPE}"
            }
        }

        stage('Execute Command') {
            steps {
                script {

                    def env = params.ENVIRONMENT

                    switch(params.SERVICE_TYPE) {

                        case 'Service user':
                            sh """
                            echo "Running Service User command on ${env}"
                            """
                            break

                        case 'Permission':
                            sh """
                            echo "Running Permission command on ${env}"
                            """
                            break

                        case 'Submission':
                            sh """
                            echo "Running Submission command on ${env}"
                            """
                            break

                        case 'B1 core':
                            sh """
                            echo "Running B1 core command on ${env}"
                            """
                            break

                        case 'F1 core':
                            sh """
                            echo "Running F1 core command on ${env}"
                            """
                            break
                    }
                }
            }
        }

    }
}