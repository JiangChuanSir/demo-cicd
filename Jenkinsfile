pipeline {
    agent any
    environment {
        HARBOR_URL = 'harbor.lanhaoyuan.top'
        IMAGE_NAME = 'demo/demo'
        IMAGE_TAG = 'v1'
    }
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
                sh "docker build -t ${HARBOR_URL}/${IMAGE_NAME}:${IMAGE_TAG} ."
            }
        }
        stage('Push Image') {
            steps {
                sh "docker login ${HARBOR_URL} -u admin -p 123"
                sh "docker push ${HARBOR_URL}/${IMAGE_NAME}:${IMAGE_TAG}"
            }
        }
        stage('Deploy to K8s') {
            steps {
                sh 'kubectl apply -f k8s/'
            }
        }
    }
}
