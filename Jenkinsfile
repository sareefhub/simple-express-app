pipeline {
    agent any
    tools {
        nodejs "NodeJS"
    }

    stages {
        stage('Build') {
            steps {
                git branch: 'feature/lab', url: 'https://github.com/sareefhub/simple-express-app.git'
                sh "npm install"
            }
        }

        stage('Scan') {
            steps {
                withSonarQubeEnv('sq1') {
                    sh "npx sonar-scanner -Dsonar.projectKey=mywebapp"
                }
            }
        }
    }
}
