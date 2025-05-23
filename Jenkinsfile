pipeline {
    agent any

    stages {
        stage('Docker Push') {
            steps {
                script {
                    withCredentials([usernamePassword(credentialsId: 'DockerHub-yanick190', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                        sh '''
                            export DOCKER_HOST=tcp://host.docker.internal:2375
                            docker login -u $USERNAME -p $PASSWORD
                            docker push yanick190/node-web-app
                        '''
                    }
                }
            }
        }
        stage('Trigger Render Deployment') {
            steps {
                script {
                    withCredentials([string(credentialsId: 'Render', variable: 'KEY')]) {
                        sh "curl https://api.render.com/deploy/$KEY"
                    }
                }
            }
        }        
    }
}
