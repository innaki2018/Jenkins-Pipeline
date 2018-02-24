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

        stage ('Deployments'){
            parallel{
                stage ('Deploy to Staging'){
                    steps {
                        sh "scp **/target/*.war innaki@innaki-VirtualBox:/home/innaki/SCP1"
                    }
                }

                stage ("Deploy to Production"){
                    steps {
                        sh "scp **/target/*.war innaki@innaki-VirtualBox:/home/innaki/SCP2"
                    }
                }
 
            }
        }
    }
}
