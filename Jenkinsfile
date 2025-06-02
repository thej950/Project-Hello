pipeline {
    agent any
    environment {
        REPO = 'https://github.com/thej950/Project-Hello.git'
        GCP_PROJECT_ID = 'glossy-premise-461511-t3'    
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
                sh 'docker build -t "$IMAGE_NAME" .'
            }
        }
        stage ('push to GCR') {
            steps {
                sh '''
                    gcloud auth configure-docker --quiet
                    docker push $IMAGE_NAME
                '''
            }
        }
    }
}




