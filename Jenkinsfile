pipeline {
    agent any

    environment {
        DOCKER_IMAGE = "sidduthatikanti93/hostel-booking"
        DOCKER_TAG   = "latest"
        DOCKER_CREDS = "dockerhub-creds"
    }

    stages {

        stage('Checkout Source') {
            steps {
                echo "Repository checked out by Jenkins SCM"
            }
        }

        stage('Build Docker Image') {
    steps {
        sh '''
        docker build -t sidduthatikanti93/hostel-booking:latest \
        -f frontend/Dockerfile frontend
        '''
    }
}


        stage('Docker Login') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: DOCKER_CREDS,
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    sh '''
                    echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                    '''
                }
            }
        }

        stage('Push Image') {
            steps {
                sh '''
                docker push $DOCKER_IMAGE:$DOCKER_TAG
                '''
            }
        }

        stage('Deploy to Azure VM') {
            steps {
                sh '''
                echo "Deploy step goes here"
                '''
            }
        }
    }

    post {
        success {
            echo "✅ Pipeline completed successfully"
        }
        failure {
            echo "❌ Pipeline failed"
        }
        always {
            sh 'docker logout || true'
        }
    }
}

