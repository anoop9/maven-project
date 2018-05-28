pipeline {
    agent any

     tools {
        maven 'localmvn'
    }

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