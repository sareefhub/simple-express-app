pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                git branch: 'feature/lab', url: 'https://github.com/sareefhub/simple-express-app.git'
                bat "npm install"
            }
        }

        stage('Scan') {
            steps {
                withSonarQubeEnv('sq1') {
                    bat 'npx sonar-scanner -Dsonar.projectKey=mywebapp'
                }
            }
        }
    }
}
