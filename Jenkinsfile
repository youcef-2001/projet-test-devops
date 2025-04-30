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
    }
}
