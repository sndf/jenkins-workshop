pipeline {
    agent {
        docker {
            image 'node:12.4-alpine'
			args '-p 3000:3000'
        }
    }
    environment {
        CI = 'true'
		USERNAME = credentials('USERNAME')
		MONGODB_CREDENTIALS = credentials('mongodb_pwd')
    }
    stages {
        stage('Build') {
            steps {
                sh 'npm install'
            }
        }
        stage('Test') {
            steps {
                sh 'npm test'
            }
        }
        stage('Deploy') {
            steps {
                sh './scripts/deploy.sh'
				input message: 'Has acabado de ver el server? (Click "Proceed" para continuar)'
				sh './scripts/kill.sh'
            }
        }
    }
}
