pipeline {
    agent any

    stages {
        stage('Clean Workspace') {
            steps {
                deleteDir()
            }
        }

        stage('Checkout SCM') {
            steps {
                git branch: 'main', credentialsId: 'id-jenkins-github', url: 'https://github.com/youcef-2001/projet-test-devops.git'
            }
        }

        stage('Build Image') {
            steps {
                script {
                    sh 'docker build -t myimage_nginx .'
                    sh 'docker tag myimage_nginx youyou:myimage_nginx'
                }
            }
        }

        stage('Deploy App') {
            steps {
                script {
                    // Supprimer l'ancienne image si elle existe
                    sh 'docker image rm -f myimage_nginx || true'

                    // Arrêter le conteneur s'il est en cours d'exécution
                    sh 'docker stop monapp || true'

                    // Supprimer le conteneur s'il existe
                    sh 'docker rm monapp || true'

                    // Lancer le nouveau conteneur
                    sh 'docker run -d --name monapp --hostname monapp -p 8089:80 myimage_nginx:youyou'
                }
            }
        }
    }
}

