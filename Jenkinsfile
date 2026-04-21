pipeline{
    agent any
    tools{
        jdk 'jdk21'
        maven 'mvn3'
    }
    stages{
        stage('Git Checkout'){
            steps{
                git branch: 'master', url: 'https://github.com/tawfeeq421/maven.git'
            }
        }
        stage('Maven Build'){
            steps{
                sh 'mvn clean package -DskipTests'
            }
        }
        stage('Deploy To QA'){
            steps{
            sh 'scp /var/lib/jenkins/workspace/docker-ci/webapp/target/webapp.war ubuntu@172.31.47.43:/var/lib/tomcat10/webapps/test.war'
            }
                }
    }
}