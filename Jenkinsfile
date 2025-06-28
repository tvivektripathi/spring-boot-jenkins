pipeline {
    // agent {
    //     docker {
    //         image 'maven:3.9.0'
    //         args '-v /root/.m2:/root/.m2'
    //     }
    // }
    agent any

    parameters{
        string(name: 'Environment', defaultValue: 'dev')
        booleanParam(name: 'RUN_TEST', defaultValue: true)
    }

    stages {
        stage('lint and format'){
            parallel{
                stage('lint') {
                    steps{
                        bat "timeout 10"
                        echo "linting stage"
                    }
                }
                stage('format'){
                    steps{
                        bat "timeout 30"
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
    }
}
