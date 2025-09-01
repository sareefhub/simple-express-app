pipeline {
    agent {
        docker {
            image 'node:18'
        }
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
