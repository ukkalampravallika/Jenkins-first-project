pipeline {
    agent any

    environment {
        // Set global variables if needed
        APP_NAME = "my-app"
        DEPLOY_ENV = "production"
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
    steps {
        echo "Starting build..."
        sh 'gradle build'
    }
}


        stage('Test') {
            steps {
                echo "Running tests..."
                sh './gradlew test' // adjust for your tech stack
            }
        }
       

        stage('Deploy') {
            steps {
                echo "Deploying to ${DEPLOY_ENV}..."
                // Example: copy artifacts to a remote server
                sh """
                    scp build/libs/${APP_NAME}.jar user@yourserver:/opt/${APP_NAME}/
                    ssh user@yourserver 'systemctl restart ${APP_NAME}'
                """
            }
        }
    }

    post {
        success {
            echo 'Build and deploy succeeded!'
        }
        failure {
            echo 'Build or deploy failed.'
        }
    }
}

