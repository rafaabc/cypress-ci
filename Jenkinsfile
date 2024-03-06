pipeline {
    agent any

    tools { nodejs 'Node21' }

    stages {
        stage('Install dependencies') {
            steps {
                sh 'npm i'
            }
        }
        stage('e2e checks') {
            steps {
                sh 'npm run cypress run'
            }
        }
    }
    post {
        always {
            junit 'results/*.xml'
        }
    }
}
