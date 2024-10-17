pipeline {
    agent any

    triggers {
        cron('H/10 * * * 1') // Trigger every 10 minutes on Mondays
    }

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "MAVEN3"
    }
    
    stages {
        stage('Build') {
            steps {
                script {
                    // Checkout code
                    checkout scm
                    
                    // Run Maven to generate artifact and run tests
                    sh 'mvn clean package'
                }
            }
        }

        stage('Code Coverage') {
            steps {
                script {
                    // Generate code coverage report with JaCoCo
                    sh 'mvn jacoco:report'
                }
            }
        }
    }

    post {
        always {
            // Archive the coverage report
            archiveArtifacts artifacts: 'target/site/jacoco/**', allowEmptyArchive: true
        }
    }
}
