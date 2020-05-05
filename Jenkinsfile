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
                    input message: 'Approve Production Deployment'
                }
                build job: 'deploy_to_prod'
            }post{
                success{
                    echo "Code deployed to prod"
                }failure{
                    echo "Deploy to prod failed"
                }
            }
        }
    }

}
