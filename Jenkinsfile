pipeline{
    agent any
    stages{
        stage("Code Checkout"){
            steps{
                git branch: 'main', credentialsId: 'demo', url: 'https://github.com/BalaramThota/doctor.git'
            }
        }
        stage("maven Build"){
            steps{
                sh 'mvn package'
            }
        }
        stage("dev deploy"){
            steps{
                sshagent(['Tomcat-dev']) {
           // copy war file from tomcat dev server
          sh "scp -o StrictHostKeyChecking=no target/doctor.war ec2-user@172.31.15.139:/opt/tomcat9/webapps/"
          //Restart Tomcatr Server
          sh "ssh ec2-user@172.31.15.139 /opt/tomcat9/bin/shutdown.sh"
          sh "ssh ec2-user@172.31.15.139 /opt/tomcat9/bin/startup.sh"
               }
            }
        }
    }
}
