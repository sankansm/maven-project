pipeline {
        agent any
        stages{
            stage('Build'){
                steps{
                sh 'mvn clean package'
                sh "docker build -t webappimage:${env.BUILD_ID} ."
                }
            }
        }

}
