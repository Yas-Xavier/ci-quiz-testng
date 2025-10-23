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

        stage('Build') {
            steps {
                echo 'Building Maven project...'
                sh 'mvn -B -q clean compile'
            }
        }

        stage('Test') {
            steps {
                echo 'Running TestNG tests...'
                sh 'mvn -B -q test'
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
