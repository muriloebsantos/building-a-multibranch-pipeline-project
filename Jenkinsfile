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
        stage('Deliver for development') {
            steps {
                when {
                    branch 'development'
                }
                sh './jenkins/scripts/deliver-for-development.sh'
                input 'Deploy para ambiente de desenvolvimento?'
                sh './jenkins/scripts/kill.sh'
            }
        }
        stage('Deliver for production') {
            steps {
                when {
                    branch 'production'
                }
                sh './jenkins/scripts/deliver-for-production.sh'
                input 'Deploy para ambiente de producao?'
                sh './jenkins/scripts/kill.sh'
            }
        }
    }
}
