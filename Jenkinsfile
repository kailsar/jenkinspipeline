pipeline {
    agent any
   

    triggers {
         pollSCM('* * * * *') // Polling Source Control
     }

stages{
        stage('Build'){
            steps {
                sh '/usr/local/bin/apache-maven-3.5.4/bin/mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

                stage ("Deploy to Production"){
                    steps {
                        sh "cp /home/jenkins/tomcat-demo.pem **/target/*.war /var/lib/tomcat8/webapps"
                    }
                }
            
        
    }
}
