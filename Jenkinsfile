pipeline {
    agent any   // Run on any available agent

    stages {
        stage('Checkout') {
            steps {
                // Clone the repository
                git url: 'https://github.com/vogash/test.git', branch: 'main'
            }
        }

        stage('Build') {
            steps {
                echo 'Building...'
                sh './gradlew build'   // Replace with your build tool (e.g., mvn, npm, make)
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                sh './gradlew test'    // Or `mvn test`, `npm test`, etc.
            }
        }

        stage('Archive') {
            steps {
                echo 'Archiving artifacts...'
                archiveArtifacts artifacts: '**/build/libs/*.jar', fingerprint: true
            }
        }
    }

    post {
        always {
            junit '**/build/test-results/test/*.xml'   // Collect test results
        }
        success {
            echo 'Pipeline completed successfully ✅'
        }
        failure {
            echo 'Pipeline failed ❌'
        }
    }
}
