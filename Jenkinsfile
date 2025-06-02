pipeline {
    agent any
    environment {
        REPO = 'https://github.com/thej950/Project-Hello.git'
    }
    stages {
        stage('Checkout') {
            steps {
                cleanWs()
                echo "Workspace cleaned. Build number: $BUILD_NUMBER"
                git url: "${REPO}"
            }
        }
    }
}
