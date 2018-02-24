pipeline {
    agent any
    
    /*parameters { 
         string(name: 'tomcat_dev', defaultValue: '127.0.1.1', description: 'Development Server')
         string(name: 'tomcat_prod', defaultValue: '127.0.1.1', description: 'Production Server')
    }
    */

    triggers {
         pollSCM('* * * * *') // Polling Source Control
     }

stages{
        stage('Build'){
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving...'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }

}
