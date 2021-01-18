pipeline {
    agent {
        label 'slave1'
    }
    environment{
        DOCKER_TAG = getDockerTag()
    }
    stages{
        stage('Build Docker Image'){
            steps{
                sh "docker build ."
                sh "docker tag $(docker image ls | grep "<none>" | awk '{print $3}') dockerpapa922\nodeapp:${DOCKER_TAG}"
            }

        }
    }
}

def getDockerTag(){
    def tag  = sh script: 'git rev-parse HEAD', returnStdout: true
    return tag
}