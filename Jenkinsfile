pipeline {
    agent any

    tools{
        maven 'localmvn'
        jdk 'localjdk'
    }


    parameters {
         string(name: 'tomcat_dev', defaultValue: '52.14.212.87', description: 'Staging Server')
         string(name: 'tomcat_prod', defaultValue: '18.191.32.119', description: 'Production Server')
    }

    triggers {
         pollSCM('* * * * *')
     }

stages{
        stage('Build'){
            steps {
                bat 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

        stage ('Deployments'){
            parallel{
             stage ('Deploy to Staging'){
                    steps {
                        bat "winscp -i /home/jenkins/tomcat-demo.pem **/target/*.war ec2-user@${params.tomcat_dev}:/var/lib/tomcat7/webapps"
                    }
                }

                stage ("Deploy to Production"){
                    steps {
                        bat "winscp -i /home/jenkins/tomcat-demo.pem **/target/*.war ec2-user@${params.tomcat_prod}:/var/lib/tomcat7/webapps"
                    }
                }
            }
        }
    }
}