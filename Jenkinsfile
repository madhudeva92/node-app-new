pipeline {
    agent any
    environment{
        DOCKER_TAG = getDockerTag()
        IMAGE_URL_WITH_TAG = "madhudeva92/node-app:${DOCKER_TAG}"
    }
    stages{
        stage('Build Docker Image'){
            steps{
                sh "docker build . -t ${IMAGE_URL_WITH_TAG}"
            }
        }
        stage('dockerhub Push'){
            steps{
		    withCredentials([string(credentialsId: 'dockerhub', variable: 'dockerhub')]) {
			    sh "docker login -u madhudeva92 -p ${dockerhub} "
			    sh "docker push ${IMAGE_URL_WITH_TAG}"
                }                     
            }
        }
    }   
}

def getDockerTag(){
    def tag  = sh script: 'git rev-parse HEAD', returnStdout: true
    return tag
}
