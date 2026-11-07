pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                dir('app') {
                    sh 'chmod +x mvnw'
                    sh './mvnw -B clean package'
                }
            }
        }

        stage('Test') {
            steps {
                echo 'Maven package completed successfully, including tests.'
            }
        }
    }

    post {
        success {
            echo 'Customer Management build completed successfully!'
        }
        failure {
            echo 'Build failed. Check the console output.'
        }
    }
}
