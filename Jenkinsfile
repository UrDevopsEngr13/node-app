pipeline {
    agent any //any available Jenkins agent
    environment{
        DOCKER_TAG = getDockerTag()
    }
    stages{
        stage('Build Docker Image'){
            steps{
                sh "docker build . -t dockerpapa922\nodeapp:$(DOCKER_TAG)"
            }

        }
    }
}

def getDockerTag(){
    def tag  = sh script: 'git rev-parse HEAD', returnStdout: true
    return tag
}