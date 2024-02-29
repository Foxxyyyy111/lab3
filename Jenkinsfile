pipeline {
    agent any

    stages {
        stage('Cleanup') {
            steps {
                sh  "docker rm -f $(docker ps -aq) || true"
                sh "docker network create network1 || true"
            }
        }



        stage('Build-stage') {
            steps {
                sh "docker build -t flaskapp ."
                sh "docker build -t mynginx -f Dockerfile.nginx ."
            
        }

        stage('Run-stage') {
            steps {
                sh "docker run -d --network network1 --name flask-app flaskapp"
                sh "docker run -d -p 80:80 --network network1 --name mycontainer mynginx"
            }
        }
    }
}
