pipeline {
    agent any

    stages {
        stage('clean workpace') {
            steps {
                deleteDir()
            }
        }
        stage('checkout SCM') {
            steps {
              sh 'git clone https://github.com/youcef-2001/projet-test-devops.git'
            }
        }

        stage('build image docker') {
            steps {
              script {
                  sh 'cd projet-test-devops'
                  sh 'docker buildx build -t mynginx-github .'
                  sh 'docker tag mynginx-github local-repo:mynginx-github'
                  
              }
            }
        }


        stage('deploiement application') {
            steps {
              script {
                    sh 'docker image rm nginx'
                    sh 'docker stop myapp'
                    sh 'docker rm myapp'
                  
                    sh 'docker rm -f $(docker ps -a)'
                    sh 'docker run -d --name myapp --hostname myapp -p 8089:80  mynginx-github'
              }
            }
        }
    }
}
