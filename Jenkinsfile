pipeline {
    agent any

    environment {
        // Define environment variables
        FLASK_APP = "app.py" // Replace with your Flask application filename
        FLASK_ENV = "production" // Environment setting (production, development, etc.)
        FLASK_RUN_HOST = "0.0.0.0" // Flask server host
        FLASK_RUN_PORT = "5000" // Flask server port
        DOCKER_REGISTRY = "" // Docker registry URL
        IMAGE_NAME = "aakash123456/flaskapp1" // Docker image name
        TAG = "latest" // Docker image tag
    }

    stages {
        stage('Clone Repository') {
            steps {
                // Checkout code from a Git repository
                git branch: 'master', url: 'https://github.com/Aakash644/Dockerize-flask-app.git'
            }
        }

       

        stage('Build Docker Image') {
            steps {
                // Example: Build Docker image
                sh '''docker build -t ${IMAGE_NAME} . '''
            }
        }

        stage('Push Docker Image') {
            steps {
              
                    // Use Jenkins credentials for Docker Hub login
                       withCredentials([usernamePassword(credentialsId: 'dockerHub', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                    script {
                        sh '''
                        echo $DOCKER_PASSWORD | docker login -u aakash123456 --password-stdin
                        docker push ${IMAGE_NAME}
                        docker logout
                        '''
                    }
                       }
            }
        }
        stage('run Docker app') {
            steps {
               sh 'docker run -d -p 5000:5000 ${IMAGE_NAME}'
               }
            }
        
      

      
        }
    }

