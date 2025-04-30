pipeline {
    agent any
    stages {
        stage('Clean Workpace') {
            steps {
                deleteDir()
            }
        }
        stage('checkout SCM') {
            steps {
                git branch: 'main', credentialsId: 'id-jenkins-github', url: 'https://github.com/youcef-2001/projet-test-devops.git'
            }
        }
        stage('Build image') {
            steps {
              script {
                  sh 'docker build -t myimage_nginx .'
                  sh 'docker tag myimage_nginx youyou:myimage_nginx'
              }
            }
        }
        stage('Deployment app') {
            steps {
               script {
                   sh 'docker image rm myimage_nginx:youyou'
                   sh 'docker stop  monapp'
                   sh 'docker rm -f $(docker ps -a)'
                   sh 'docker run -d --name monapp --hostname monapp -p 8089:80 myimage_nginx'
                   sh'docker exec -ti monapp '
               }
            }
        }
    }
}
