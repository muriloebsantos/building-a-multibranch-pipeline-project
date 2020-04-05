pipeline {
    agent {
        docker {
            image 'node:6-alpine'
            args '-p 3000:3000 -p 50000:50000'
        }
    }
    environment {
        CI = true
    }
    stages {
        stage('Build') {
            steps {
                sh 'echo "instalando dependencias"'
                sh  'npm install'
            }
        }
        stage('Test') {
            steps {
                sh 'echo "realizando testes. poderia rodar jenkins/scripts/test.sh para deixar mais limpo"'
                sh 'npm test'
            }
        }
    }
}
