pipeline {
    agent any

    stages {

        stage('Debug Env') {
            steps {
                sh 'id'
                sh 'whoami'
                sh 'groups'
                sh 'hostname'
                sh 'ls -l /var/run/docker.sock'
                sh 'docker version || true'
            }
        }

        stage('Clone') {
            steps {
                git url: 'git@github.com:JiangChuanSir/demo-cicd.git',
                    credentialsId: 'github-ssh',
                    branch: 'main'
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
