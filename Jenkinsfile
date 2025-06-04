pipeline {
    agent any
    // defining environment variables 
    environment {
        REPO = 'https://github.com/thej950/Project-Hello.git'
        GCP_PROJECT_ID = 'glossy-premise-461511-t3'    // project id in GCP account 
        IMAGE_NAME = "gcr.io/${GCP_PROJECT_ID}/project-hello" //Image name 
        CLUSTER_NAME = 'hello-project-k8s-cluster' // cluster name 
        CLUSTER_ZONE = 'us-central1-c' // cluster zone 
        DEPLOYMENT_FILE = 'deployment.yml'
        
    }
    stages {
        stage('Checkout') {
            steps {
                cleanWs() // it will clean workspace every new build
                echo "Workspace cleaned. Build number: $BUILD_NUMBER" //pre-defined variables 
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
        // Below step is important to remove old images
        stage ('Remove docker images') {
            steps {
                sh 'docker system prune -af'
            }
        }
        stage ('GKE Cluster Authenticate') {
            steps {
                sh '''
                    echo "======= Getting credentials for GKE cluster.======="
                    gcloud container clusters get-credentials "$CLUSTER_NAME" --zone "$CLUSTER_ZONE" --project "$GCP_PROJECT_ID"
                '''
            }
        }
        stage ('application deploy into GKE') {
            steps {
                sh 'kubectl apply -f "$DEPLOYMENT_FILE"'
            }
        }
        stage ('Verify pods service IP') {
            steps {
                sh 'kubectl get nodes'
                sh 'kubectl get pods && kubectl get svc'
                sh 'ls -la'
            }
        }
    }
}




