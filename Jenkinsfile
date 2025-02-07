pipeline {
    agent any

    environment {
        BUILD_ARTIFACT = "my-app.jar"
    }

    stages {
        stage('Clone Repository') {
            steps {
                  git branch: 'main', url: 'https://github.com/aravind-zinnect/simple-repo3.git'
            }
        }

        stage('Build with Maven') {
            steps {
                script {
                    bat 'mvn clean package'
                }
            }
        }

        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
            }
        }

        stage('Deploy to Web Server') {
            steps {
                script {
                    bat 'copy target\\my-app.jar C:\\apache-web-server\\deploy\\'
                }
            }
        }

        stage('Post-Build Actions') {
            steps {
                mail to: 'your-email@example.com',
                     subject: "Jenkins Build: ${currentBuild.fullDisplayName}",
                     body: "Build completed successfully! Check artifacts."
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}
