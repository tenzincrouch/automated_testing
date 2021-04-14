pipeline {
    agent {
        docker {
            image 'maven:3-alpine'
            args '-v /root/.m2:/root/.m2'
        }
    }

    stages {
        stage('Build') {
            steps {
                git 'https://github.com/tenzincrouch/automated_testing.git'
                sh 'mvn clean compile'

            }
        }

        stage('Test') {
             steps {
                sh 'mvn test'
                junit 'src/reports/*-jupiter.xml'
             }
        }
    }
}
