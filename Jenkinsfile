pipeline {
    agent any
    stages {
        stage('Build Jar') {
            steps {
                bat 'mvn clean package -DskipTests'
            }
        }
        stage('Build Image') {
            steps {
                script {
                	bat "docker build -t='3220/selenium-docker' ."
                }
            }
        }
        stage('Push Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'pass', usernameVariable: 'user')]
                bat "docker login --username=${user} --password=${pass}"
                bar "docker push 3220/selenium-docker:latest"
            }
        }
    }
}