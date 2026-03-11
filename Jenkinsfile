pipeline {

    agent any

    environment {
        IMAGE = "devops-lab-app"
    }

    stages {

        stage('Checkout Code') {
    steps {
        git branch: 'main', url: 'https://github.com/hnj1994/devops-lab-app.git'
    }
}
        stage('Build Docker Image') {
            steps {
                sh 'docker build -t devops-lab-app:${BUILD_NUMBER} .'
            }
        }

        stage('Deploy Application') {
            steps {
                sh '''
                ssh admin@10.22.18.227 "
                docker stop devops-container || true &&
                docker rm devops-container || true &&
                docker run -d -p 4000:3000 --name devops-container devops-lab-app:${BUILD_NUMBER}
                "
                '''
            }
        }

    }
}
