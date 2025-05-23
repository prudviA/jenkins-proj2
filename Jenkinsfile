pipeline {
    agent any

    environment {
        IMAGE_NAME = "nodejs-cicd"
        CONTAINER_NAME = "nodejs-cicd-container"
    }

    stages {
        // Removed unnecessary 'Clone Repo' stage

        stage('Install Dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'npm test'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh "docker build -t $IMAGE_NAME ."
            }
        }

        stage('Remove Old Container') {
            steps {
                sh "docker rm -f $CONTAINER_NAME || true"
            }
        }

        stage('Run New Container') {
            steps {
                sh "docker run -d -p 3000:3000 --name $CONTAINER_NAME $IMAGE_NAME"
            }
        }
    }

    post {
        success {
            echo 'Deployment successful'
        }
        failure {
            echo 'Build failure'
        }
    }
}
