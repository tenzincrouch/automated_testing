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
                junit '**/target/surefire-reports/TEST-*.html'
             }
        }

        stage('Static Analysis') {
            steps{
                withSonarQubeEnv(credentialsId: 'sonarqube-id', installationName: 'local') {
                    sh 'mvn verify org.sonarsource.scanner.maven:sonar-maven-plugin:sonar'
                }
            }
        }

        stage('Report') {
              steps {
                sh 'mvn site'
                publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, includes: '**/*.html,**/*.css',
                             keepAll: true, reportDir: 'target/site', reportFiles: 'index.html',
                             reportName: 'Unit Testing Report', reportTitles: 'index.html'])
              }
        }
    }
}
