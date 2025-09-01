pipeline {
    agent any

    tools {
        nodejs "Node18"
    }

    stages {
        stage('Checkout Code') {
            steps {
                echo "📥 Checking out source code..."
                git branch: 'feature/lab', url: 'https://github.com/sareefhub/simple-express-app.git'
            }
        }

        stage('Build') {
            steps {
                echo "⚙️ Installing dependencies..."
                sh "node -v"
                sh "npm -v"
                sh "npm install"
            }
        }

        stage('SonarQube Scan') {
            steps {
                echo "🔍 Running SonarQube analysis..."
                withSonarQubeEnv('sq1') {
                    script {
                        def scannerHome = tool 'SonarScanner4'
                        sh """
                            ${scannerHome}/bin/sonar-scanner \
                            -Dsonar.projectKey=mywebapp \
                            -Dsonar.sources=. \
                            -Dsonar.sourceEncoding=UTF-8
                        """
                    }
                }
            }
        }

        stage('Quality Gate') {
            steps {
                echo "🚦 Checking SonarQube Quality Gate..."
                timeout(time: 30, unit: 'SECONDS') {
                    script {
                        def qg = waitForQualityGate abortPipeline: true
                        echo "Quality Gate status: ${qg.status}"
                    }
                }
            }
        }
    }
}
