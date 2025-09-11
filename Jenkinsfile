pipeline {
    agent {label 'devops1-ardyan'}
    
    

    stages {
        stage('Checkout SCM') {
            steps {
                git branch: 'main', url: 'https://github.com/GitKintel/simple-apps.git'
            }
        }
        stage('Build') {
            steps {
                sh '''cd apps
                npm install'''
            }
        }
        stage('Testing') {
            steps {
                sh '''cd apps
                npm test
                npm run test:coverage'''
            }
        }
        stage('Code Review') {
            steps {
                sh '''cd apps
                sonar-scanner \
                -Dsonar.projectKey=simple-apps \
                -Dsonar.sources=. \
                -Dsonar.host.url=http://172.23.13.202:9000 \
                -Dsonar.login=sqp_636819eea3ff8d5f9db00374ab3dc1d0404470c96'''
            }
        }
        stage('Deploy compose') {
            steps {
                sh '''
                docker compose build
                docker compose up -d
                '''
            }
        }
    }
}