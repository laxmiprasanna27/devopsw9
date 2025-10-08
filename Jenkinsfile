pipeline {
    agent any
    stages {
        stage("Build Docker image") {
            steps {
                echo "Build Docker image"
                bat "docker build -t kubdemoapp:v1 ."
            }
        }
        stage("Docker Login") {
            steps {
                bat "docker login -u laxmiprasanna11 -p laxmiprasanna@11"
            }
        }
        stage("Push Docker image to Docker Hub") {
            steps {
                echo "Push Docker image to Docker Hub"
                bat "docker tag kubdemoapp:v1 laxmiprasanna11/week8:t1"
                bat "docker push laxmiprasanna11/week8:t1"
            }
        }
        stage("Deploy to Kubernetes") {
            steps {
                echo "Deploy to Kubernetes"
                bat "kubectl apply -f deployment.yaml --validate=false"
                bat "kubectl apply -f service.yaml"
            }
        }
    }
    post {
        success {
            echo "Pipeline executed successfully"
        }
        failure {
            echo "Pipeline failed. Please check the logs."
        }
    }
}
