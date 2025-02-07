pipeline {
    agent any

    environment {
        BUILD_ARTIFACT = "my-app.jar"
        JAVA_HOME = "C:\\Program Files\\Java\\jdk-17"
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
                    withEnv(["JAVA_HOME=${env.JAVA_HOME}", "PATH=${env.JAVA_HOME}\\bin;${env.PATH}"]) {
                        bat 'mvn clean package'
                    }
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
                    bat """
                    if not exist C:\\apache-web-server\\deploy mkdir C:\\apache-web-server\\deploy
                    copy target\\my-app.jar C:\\apache-web-server\\deploy\\
                    """
                }
            }
        }

        stage('Post-Build Actions') {
            steps {
                script {
                    emailext(
                        to: 'your-email@example.com',
                        subject: "Jenkins Build: ${currentBuild.fullDisplayName}",
                        body: "Build completed successfully! Check artifacts at http://your-server-url/deploy/"
                    )
                }
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}
