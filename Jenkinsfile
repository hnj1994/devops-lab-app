pipeline {

    agent any

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
                docker save devops-lab-app:${BUILD_NUMBER} | ssh admin@10.22.18.228 docker load

                ssh admin@10.22.18.228 "
                docker stop devops-container || true &&
                docker rm devops-container || true &&
                docker run -d -p 3000:4000 --name dell003-container devops-lab-app:${BUILD_NUMBER}
                "
                '''
            }
        }

    }
}
