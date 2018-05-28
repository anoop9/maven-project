pipeline {
    agent any

     tools {
        maven 'localmvn'
    }
     tools {
        jdk 'localjdk'
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