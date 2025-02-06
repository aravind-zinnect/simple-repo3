pipeline {
    agent any

    stages {
       stage('Clone Repository') {
    steps {
        git branch: 'main', url: 'https://github.com/aravind-zinnect/simple-repo3'
    }
}


        stage('Create Artifact') {
            steps {
                script {
                    // Create a simple text file
                    bat 'echo This is my Jenkins artifact file > my_artifacts_report.txt'
                }
            }
        }

        stage('Archive Artifacts') {
            steps {
                archiveArtifacts artifacts: 'my_artifacts_report.txt', fingerprint: true
            }
        }
    }
}
