pipeline {
    agent any

    tools {
        jdk 'jdk21'
        maven 'mvn3'
    }

    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/tawfeeq421/maven.git'
            }
        }

        stage('Maven Build') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Deploy To QA') {
            steps {
                sh '''
                scp -o StrictHostKeyChecking=no \
                $WORKSPACE/webapp/target/webapp.war \
                ubuntu@172.31.47.43:/var/lib/tomcat10/webapps/test.war
                '''
            }
        }
    }

    post {
        success {
            slackSend(
                channel: '#maven',
                color: 'good',
                message: "✅ SUCCESS: ${env.JOB_NAME}#${env.BUILD_NUMBER}"
            )
        }

        failure {
            slackSend(
                channel: '#maven',
                color: 'danger',
                message: "❌ FAILURE: ${env.JOB_NAME}#${env.BUILD_NUMBER}\nSee Logs: ${env.BUILD_URL}"
            )
        }

        always {
            echo 'Pipeline finished'
        }
    }
}