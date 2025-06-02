pipeline {
    agent any
    environment {
        REPO = 'https://github.com/thej950/Project-Hello.git'
        GCP_PROJECT_ID = 'your-gcp-project-id'     // Replace with your actual project ID
        IMAGE_NAME = "gcr.io/${GCP_PROJECT_ID}/project-hello"
    }
    stages {
        stage('Checkout') {
            steps {
                cleanWs()
                echo "Workspace cleaned. Build number: $BUILD_NUMBER"
                git url: "${REPO}", branch: 'main'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t myimage ."
            }
        }
    }
}
