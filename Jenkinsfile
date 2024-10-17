pipeline {
    agent any

    triggers {
        cron('H/10 * * * 1')  // Trigger every 10 minutes on Mondays
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout code from your GitHub repo
                git url: 'https://github.com/your-account/your-repo.git', branch: 'main'
            }
        }

        stage('Build') {
            steps {
                // Run your build steps here, e.g., Maven or Gradle
                sh './gradlew build'
            }
        }

        stage('Code Coverage') {
            steps {
                // Use Jacoco to generate the coverage report
                jacoco execPattern: '**/build/jacoco/test.exec', 
                       classPattern: '**/classes',
                       sourcePattern: '**/src/main/java', 
                       exclusionPattern: '**/src/test*'
            }
        }

        stage('Archive Artifacts') {
            steps {
                // Archive the generated artifacts
                archiveArtifacts artifacts: '**/build/libs/*.jar', fingerprint: true
            }
        }
    }

    post {
        always {
            // Actions to perform after pipeline runs (e.g., cleanup)
            cleanWs()
        }
    }
}
