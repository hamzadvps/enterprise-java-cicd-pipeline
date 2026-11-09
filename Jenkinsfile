pipeline {
    agent any

    stages {
        stage('Build and Test') {
            steps {
                dir('app') {
                    sh 'chmod +x mvnw'
                    sh './mvnw -B clean verify'
                }
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    dir('app') {
                        sh './mvnw -B org.sonarsource.scanner.maven:sonar-maven-plugin:5.1.0.4751:sonar -Dsonar.projectKey=Customer-Management'
                    }
                }
            }
        }
    }

    post {
        success {
            echo 'Build, tests and SonarQube analysis completed!'
        }
        failure {
            echo 'Pipeline failed. Check the console output.'
        }
    }
}
