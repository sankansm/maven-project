pipeline {
    agent any

    stages{
        stage('Build'){
            steps{
                sh 'mvn clean package'
            }
            post{
                success{
                    archiveArtifacts artifacts: '**/**/*.war'
                }
            }
        }
        stage('Deploy to Staging'){
             steps{
                 build job: 'deploy_to_staging'
             }

        }
    }
}
