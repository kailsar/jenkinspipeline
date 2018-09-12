pipeline {
    agent any
    
    parameters { 
         string(name: 'tomcat_dev', defaultValue: '35.178.204.224', description: 'Staging Server')
         string(name: 'tomcat_prod', defaultValue: '35.178.204.224', description: 'Production Server')
    } 

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
                        sh "scp -i /home/jenkins/tomcat-demo.pem **/target/*.war ec2-user@${params.tomcat_prod}:/var/lib/tomcat8/webapps"
                    }
                }
            
        
    }
}
