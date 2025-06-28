pipeline {
    // agent {
    //     docker {
    //         image 'maven:3.9.0'
    //         args '-v /root/.m2:/root/.m2'
    //     }
    // }
    agent any


    stages {
        stage('lint and format'){
            parallel{
                stages{
                    stage('lint'){
                        steps{
                            bat "sleep 30"
                            echo "linting stage"
                        }
                    }
                    stage('format'){
                        steps{
                            bat "sleep 30"
                            echo "formatting stage"
                        }
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
