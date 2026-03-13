pipeline {
    agent any

    environment {
        DOCKER_HUB_USER = 'piobookz'
        IMAGE_NAME = 'finead-todo-app'
        FULL_IMAGE_NAME = "${DOCKER_HUB_USER}/${IMAGE_NAME}:latest"
        DOCKER_HUB_CREDS = 'jenkins-user-for-ead'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building the application...'

                echo 'Installing backend dependencies...'
                dir('TODO/todo_backend') {
                    sh 'npm install'
                }

                echo 'Installing frontend dependencies...'
                dir('TODO/todo_frontend') {
                    sh 'npm install'
                }

                echo 'Building frontend...'
                dir('TODO/todo_frontend') {
                    sh 'npm run build'
                }

                echo 'Moving frontend build to backend...'
                sh '''
                    mkdir -p TODO/todo_backend/static
                    cp -r TODO/todo_frontend/build/* TODO/todo_backend/static/
                '''
                
                echo 'Build stage completed!'
            }
        }
        stage('Containerise') {
        steps {
            echo 'Creating Docker image...'
        
            // Build the image using the Dockerfile in todo_backend directory
            dir('TODO/todo_backend') {
                sh "docker build -t ${DOCKER_HUB_USER}/${IMAGE_NAME}:latest ."
            }
            echo 'Docker image created successfully!'
        }
}
        stage('Push') {
            steps {
                echo 'Logging into Docker Hub and pushing image...'

                withCredentials([usernamePassword(
                    credentialsId: "${DOCKER_HUB_CREDS}", 
                    passwordVariable: 'DOCKER_PASS', 
                    usernameVariable: 'DOCKER_USER'
                )]) {
                    sh "echo \$DOCKER_PASS | docker login -u \$DOCKER_USER --password-stdin"
                    sh "docker push ${DOCKER_HUB_USER}/${IMAGE_NAME}:latest"
                }
                
                echo 'Docker image pushed to Docker Hub successfully!'
            }
        }
    }
}