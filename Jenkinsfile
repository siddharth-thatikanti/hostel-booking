pipeline {
  agent any

  stages {
    stage('Clone Repo') {
      steps {
        git 'https://github.com/siddharth-thatikanti/hostelbooking.git'
      }
    }

    stage('Build Docker Image') {
      steps {
        sh 'docker build -t sidduthatikanti93/hostel-booking:latest docker/'
      }
    }

    stage('Push Image') {
      steps {
        sh 'docker push sidduthatikanti93/hostel-booking:latest'
      }
    }

    stage('Deploy to Azure VM') {
      steps {
        sh '''
        ssh azureuser@<PUBLIC_IP> << EOF
        docker pull sidduthatikanti/hostel-booking:latest
        docker stop hostel-booking || true
        docker rm hostel-booking || true
        docker run -d -p 80:80 --name hostel-booking sidduthatikanti93/hostel-booking:latest
        EOF
        '''
      }
    }
  }
}
