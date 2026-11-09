
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

        stage('Quality Gate') {
            steps {
                timeout(time: 5, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }

    post {
        success {
            echo 'Build, tests, SonarQube analysis and Quality Gate completed!'
        }
        failure {
            echo 'Pipeline failed. Check the console output.'
        }
    }
}

