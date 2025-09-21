pipeline {
    agent any

    environment {
        IMAGE_NAME = "my-httpd-image"
        CONTAINER_NAME = "my-httpd-container"
        HOST_PORT = "8081"
    }

    stages {
        stage('GitHub Checkout') {
            steps {
                // Pull code from your GitHub repo
                git branch: 'main', url: 'https://github.com/ajaytechryver/Docker-httpd-demo.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                // Build Docker image from Dockerfile
                sh "docker build -t $IMAGE_NAME ."
            }
        }

        stage('Run Docker Container') {
            steps {
                // Stop and remove any existing container if it exists
                sh '''
                if [ $(docker ps -a -q -f name=$CONTAINER_NAME) ]; then
                    docker rm -f $CONTAINER_NAME
                fi
                docker run -d --name $CONTAINER_NAME -p $HOST_PORT:80 $IMAGE_NAME
                '''
            }
        }
    }

    post {
        success {
            echo "✅ Deployment successful! Access your website at http://<server-ip>:$HOST_PORT"
        }
        failure {
            echo "❌ Pipeline failed!"
        }
    }
}

