pipeline {
    agent any

    tools {
        maven 'Maven 3.9.9'
        // Uncomment if you have a JDK tool configured in Jenkins:
        // jdk 'JDK 24'
    }

    options { 
        timestamps()
    }

    triggers {
        // This allows GitHub pushes to trigger the pipeline automatically
        githubPush()
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Cloning repository...'
                checkout scm
            }
        }

        stage('Test') {
            steps {
                echo 'Running TestNG tests...'
                bat 'mvn -B -q test'
            }
            post {
                always {
                    junit '**/target/surefire-reports/*.xml'
                }
            }
        }

        stage('Summary') {
            steps {
                echo '✅ Build and tests completed successfully!'
            }
        }
    }
}
