pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo "Building the application..."
                sh 'echo "Build step completed"'
            }
        }
        stage('Test') {
            steps {
                echo "Running tests..."
                sh 'echo "All tests passed!"'
            }
        }
        stage('Deploy') {
            steps {
                echo "Deploying the app..."
                sh 'echo "App deployed successfully!"'
            }
        }
    }
    post {
        always {
            echo "Pipeline finished."
        }
    }
}
