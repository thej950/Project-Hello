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
        // add jenkins user into docker group 
        // restart Jenkins-VM 
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t "$IMAGE_NAME" .'
            }
        }
        // Here authenticate ggogle 
        // create service account with admin privilleges to artifactory registry 
        //attch to Jenkins-VM 
        stage ('push to GCR') {
            steps {
                sh '''
                    gcloud auth configure-docker --quiet
                    docker push $IMAGE_NAME
                '''
            }
        }
        // Below command is important to remove old images
        stage ('Remove docker images') {
            steps {
                sh 'docker system prune -af'
            }
        }
    }
}




