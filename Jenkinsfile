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
            stages{
                stage('lint'){
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
                cmd 'mvn -B -DskipTests clean package'
            }
        }
        stage('Test') {
            steps {
                cmd 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
    }
}
