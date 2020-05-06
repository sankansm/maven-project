pipeline {
        agent any
        stages{
            stage('Build'){
                steps{
                sh 'mvn clean package'
                
                }
            }
            stage('Docker-Image'){
                steps{
                sh "docker build . -t webappimage:${env.BUILD_ID}"
                sh "docker tag localhost:5000/webappimage:${env.BUILD_ID}"
                sh "docker push localhost:5000/webappimage:${env.BUILD_ID}"

                }
            }
            stage('Deploy'){
                steps{
                    input message: "Approve the Deploy?"
                    sh "docker run -d -p 8081:8080 --name webapp localhost:5000/webappimage:${env.BUILD_ID}"
                }
            }
        }

}
