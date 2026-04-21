pipeline{
    agent any
    tools{
        jdk 'jdk21'
        maven 'mvn3'
    }
    stages{
        stge('Git Checkout'){
            steps{
                git branch: 'master', url: 'https://github.com/tawfeeq421/maven.git'
            }
        }
    }
}