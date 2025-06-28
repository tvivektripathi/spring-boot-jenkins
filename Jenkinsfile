pipeline {
    // agent {
    //     docker {
    //         image 'maven:3.9.0'
    //         args '-v /root/.m2:/root/.m2'
    //     }
    // }
    agent any

    parameters{
        string(name: 'PERSON', defaultValue: 'Vivek Tripathi')
        booleanParam(name: 'RUN_TEST', defaultValue: true)
        choice(name: 'ENVIRONMENT', choices: ['dev', 'test', 'staging', 'production'])
        password(name: 'PASSWORD', defaultValue: 'SECRET')
    }

    stages {
        stage('lint and format'){
            parallel{
                stage('lint') {
                    steps{
                        echo "linting stage"
                    }
                }
                stage('format'){
                    steps{
                        echo "formatting stage"
                    }
                }
            }
        }
        stage('Build') {
            steps {
                bat 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            when{
                expression{
                    params.RUN_TEST == true
                }
            }
            steps {
                bat 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Deploy'){
            steps{
                echo "Deploying to ${params.ENVIRONMENT}"
            }
        }
    }
}
