pipeline{
    agent any
    stages{
        stage("code checkout"){
            steps{
                git branch: 'main', credentialsId: 'jenkins', url: 'https://github.com/BalaramThota/doctor.git'
            }
        }
         stage("Maven Build"){
            steps{
                sh 'mvn package'
            }
        }
        stage("dev deploy"){
            steps{
                sshagent(['doctor']) {
                //copy war file to tomcat server
                 sh "scp -o StrictHostKeyChecking=no target/doctor.war ec2-user@172.31.28.234:/opt/tomcat9/webapps/"
                 //Restart tomcat server
            sh "ssh ec2-user@172.31.28.234 /opt/tomcat9/bin/shutdown.sh"
            sh "ssh ec2-user@172.31.28.234 /opt/tomcat9/bin/startup.sh"
                }
            }
        }
    }
}
