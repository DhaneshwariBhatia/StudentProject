pipeline {
    agent any  // Runs on any available Jenkins agent

    environment {
        DOCKER_IMAGE = 'your-dockerhub-username/studentproject'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/your-username/StudentProject.git'  // Change to your repo URL
            }
        }
        
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t $DOCKER_IMAGE .'
            }
        }

        stage('Push to Docker Hub') {
            steps {
                withDockerRegistry([credentialsId: 'docker-hub-credentials', url: '']) {
                    sh 'docker push $DOCKER_IMAGE'
                }
            }
        }

        stage('Deploy Container') {
            steps {
                sh 'docker run -p 8000:8000 -d $DOCKER_IMAGE'
            }
        }
    }
}
