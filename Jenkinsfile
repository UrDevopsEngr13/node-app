pipeline {
    agent any //any available Jenkins agent
    stages{
        stage('Build Docker Image'){
            steps{
                sh "docker build . -t dockerpapa922\nodeapp:latest"
            }

        }
    }
}