pipeline {
    agent any
    tools {
        nodejs "Node18"
    }

    stages {
        stage('Build') {
            steps {
                git branch: 'feature/lab', url: 'https://github.com/sareefhub/simple-express-app.git'
                sh "node -v"
                sh "npm -v"
                sh "npm install"
            }
        }

        stage('Scan') {
            steps {
                withSonarQubeEnv('sq1') {
                    script {
                        def scannerHome = tool 'SonarScanner4'
                        sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=mywebapp"
                    }
                }
            }
        }

        stage('Quality Gate') {
            steps {
                timeout(time: 1, unit: 'MINUTES') {
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }
}
