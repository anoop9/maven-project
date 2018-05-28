pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                bat 'mvn clean package'
            }
            post {
                success{
                    echo 'Archiving...'
                    archiveArtifacts  artifacts: '**/target/*.war'
                }
            }

        }
    }
}