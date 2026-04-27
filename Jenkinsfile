pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
                git url: 'git@github.com:JiangChuanSir/demo-cicd.git'
            }
        }

        stage('Build Image') {
            steps {
                sh 'docker build -t demo:v1 .'
            }
        }

        stage('Deploy to K8s') {
            steps {
                sh 'kubectl apply -f k8s/'
            }
        }
    }
}
