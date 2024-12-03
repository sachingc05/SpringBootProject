pipeline {
    agent any

    environment {
        GRADLE_HOME = './gradlew' // Gradle wrapper script
    }

    stages {
        stage('Checkout') {
            steps {
                // Pull the code from SCM
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Building the application...'
                sh "${GRADLE_HOME} clean build"
            }
        }

        stage('Test') {
            steps {
                echo 'Running unit tests...'
                sh "${GRADLE_HOME} test"
            }
        }

        stage('Package') {
            steps {
                echo 'Packaging the application...'
                sh "${GRADLE_HOME} assemble"
            }
        }

        stage('Static Code Analysis') {
            steps {
                echo 'Running static code analysis with Checkstyle...'
                sh "${GRADLE_HOME} check"
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application...'
                // Add deployment commands here, e.g., copy files, run Docker commands, etc.
                echo "Deploy completed for branch ${env.BRANCH_NAME}."
            }
        }
    }

    post {
        always {
            echo 'Cleaning up workspace...'
            cleanWs() // Clean workspace after the build
        }
        success {
            echo 'Build completed successfully!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}
