
pipeline {
    agent any

    environment {
        GCP_PROJECT = 'your-gcp-project-id'
        IMAGE_NAME = "gcr.io/${GCP_PROJECT}/hello-node"
        GCP_CREDENTIALS = 'gcp-creds'
        CLUSTER_NAME = 'hello-cluster'
        CLUSTER_ZONE = 'us-central1-a'
    }

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/thej950/Project-Hello.git'
                sh 'ls -la'
            }
        }

//         stage('Authenticate with GCP') {
//             steps {
//                 withCredentials([file(credentialsId: "${GCP_CREDENTIALS}", variable: 'GOOGLE_APPLICATION_CREDENTIALS')]) {
//                     sh '''
//                         gcloud auth activate-service-account --key-file=$GOOGLE_APPLICATION_CREDENTIALS
//                         gcloud config set project $GCP_PROJECT
//                     '''
//                 }
//             }
//         }

//         stage('Build Docker Image') {
//             steps {
//                 sh 'docker build -t $IMAGE_NAME .'
//             }
//         }

//         stage('Push to GCR') {
//             steps {
//                 sh '''
//                     gcloud auth configure-docker --quiet
//                     docker push $IMAGE_NAME
//                 '''
//             }
//         }

//         stage('Deploy to GKE') {
//             steps {
//                 withCredentials([file(credentialsId: "${GCP_CREDENTIALS}", variable: 'GOOGLE_APPLICATION_CREDENTIALS')]) {
//                     sh '''
//                         gcloud auth activate-service-account --key-file=$GOOGLE_APPLICATION_CREDENTIALS
//                         gcloud container clusters get-credentials $CLUSTER_NAME --zone $CLUSTER_ZONE --project $GCP_PROJECT
//                         kubectl apply -f deployment.yaml
//                     '''
//                 }
//             }
//         }
//     }

//     post {
//         success {
//             echo "Deployed to GKE successfully!"
//         }
//         failure {
//             echo "Something went wrong during deployment!"
//         }
    }
}
