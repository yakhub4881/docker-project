pipeline{
    agent any
    stages
    {
        stage ("checkout from SCM")
        {
            steps
            {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/yakhub4881/docker-project.git']]])
            }
        }
        stage ("build docker image")
        {
            steps{
                sh 'docker build -t nginximage:v1.$BUILD_ID .'
            }
        }
        stage ("push image to docker hub")
        {
            steps{
                withCredentials([string(credentialsId: 'Docker-Hub', variable: 'Docker-Hub-Credentials')]) {
                sh "docker login -u yakhub4881 -p ${Docker-Hub-Credentials}"
                sh 'docker tag nginximage:v1.$BUILD_ID yakhub4881/nginximage:v1.$BUILD_ID'
                sh 'docker push yakhub4881/nginximage:v1.$BUILD_ID'
                 }
            }
        }
    }
}
