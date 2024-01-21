pipeline {
    agent any
    environment {
         path="$PATH:/opt/apache-maven-3.6.3/bin"
    }    
    stages{
        stage('Getcode'){
            steps{
                git branch: 'main', url: 'https://github.com/Akshay-c-bhoyar/maven-web-app.git'    
            }   
        }
        stage('build'){
            steps{
                sh'mvn clean package'
            }
        }
        // stage('sonarqube analysis'){
        //     steps{
        //         withsonarcube Env('sonar-server-7.8'){
        //         sh "mvn sonar:sonar-7.8"
        //         }
        //     } 
        // }

        stage('Deploy'){
            steps{
		sshagent(['Tomcat-server-Agent']){                                                     
		     sh'scp -o strictHostkeychecking=no target/01-maven-app.war ec2-user@34.219.242.94:/home/ec2-user/apache-tomcat-9.0.84/webapps'
                }              
            }
        }
    }
}