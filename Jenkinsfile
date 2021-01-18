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
                sh "docker build . --tag dockerpapa922/nodeapp:${DOCKER_TAG}"
            }            
        }
        stage('Docker-Hub Push'){
            steps{
                withCredentials([string(credentialsId: 'docker-hub-access', variable: 'dockerHubPwd')]) {
                    sh ('docker login -u dockerpapa922 -p ${dockerHubPwd}')
                    sh ('docker push dockerpapa922/nodeapp:${DOCKER_TAG}')
                }                     
            }
        }
        stage('Deploy to K8s'){
            steps{
                //sh ('chmod +x changeTag.sh')
                //sh ('./changeTag.sh ${DOCKER_TAG}')
                script{
                    kubernetesDeploy(
                        configs: 'node-app-pod.yml', 
                        kubeconfigId: 'K8S', 
                        enableConfigSubstition: true
                    ) 
                }
            }
        }
    }
}

def getDockerTag(){
    def tag  = sh script: 'git rev-parse HEAD', returnStdout: true
    return tag
}