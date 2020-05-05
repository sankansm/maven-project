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
        
        stage('Deploy to prod'){
            steps{

                {
                    input message: 'Approve deploy to prod'
                }
                build job: 'deploy_to_prod'
            }
            post{
                success{
                    echo 'Deploy completed to prod'
                }
                failure {
                    echo 'deploy failed in prod'
                }
            }

        }
    }

}
