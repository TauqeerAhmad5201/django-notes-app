pipeline {
    agent any

    stages {
        stage('Cloning the code') {
            steps {
                echo "Cloning the Code"
                git branch: 'main', url: "https://github.com/TauqeerAhmad5201/django-notes-app"
            }
        }
        stage('Building the code') {
            steps {
                echo "Building the Code using Docker"
                sh "docker build -t noteapp ."
            }
        }
        stage('Pushing to Docker Hub') {
            steps {
                echo 'Pushing to Docker Hub'
                withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'dockerhubPass', usernameVariable: 'dockerhubUser')]){
                sh "docker login -u ${env.dockerhubUser} -p ${env.dockerhubPass}"
                sh "docker tag noteapp ${env.dockerhubUser}/noteapp:latest"
                sh "docker push ${env.dockerhubUser}/noteapp:latest"
                }
            }
        }
        stage('Deployment') {
            steps {
                sh "docker compose down && docker compose up -d"
            }
        }
        
        
    }
}
