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
                sh "docker tag webappimage:${env.BUILD_ID} localhost:5000/webappimage:${env.BUILD_ID}"
                sh "docker push localhost:5000/webappimage:${env.BUILD_ID}"

                }
            }
            stage('Deploy'){
                steps{
                    input message: "Approve the Deploy?"
                     sh "docker rm -f webapp"
                    sh "docker run -d -p 8090:8080 --name webapp localhost:5000/webappimage:${env.BUILD_ID}"
                }
            }
        }

}
