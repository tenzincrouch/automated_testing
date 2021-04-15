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
                //junit '**/target/surefire-reports/TEST-*.xml'
             }
        }

        stage('Static Analysis') {
            steps{
                sh 'ls'
//                 withSonarQubeEnv {
//                     sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:4.6.0.2311:sonar'
//                 }
            }
        }
    }
}
