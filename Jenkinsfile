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
                sh 'mvn surefire-report:report'

                //junit '**/target/surefire-reports/TEST-*.html'
             }
        }

        stage('Static Analysis') {
            steps{
//                 withSonarQubeEnv(credentialsId: 'sonarqube-id', installationName: 'local') {
//                     sh 'mvn verify org.sonarsource.scanner.maven:sonar-maven-plugin:sonar'
//                 }
                 sh 'mvn sonar:sonar \
                          -Dsonar.projectKey=io.michaelcane:bestcalculator \
                          -Dsonar.host.url=http://192.168.0.236:9000 \
                          -Dsonar.login=9c9391b7bdfa00837a7adfd2ae879dbe890d123c'
            }
        }
    }
}
