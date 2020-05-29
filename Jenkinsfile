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
                sh "docker build . -t webappimage:${BUILD_NUMBER}"
                sh "docker tag webappimage:${env.BUILD_ID} localhost:5000/webappimage:${BUILD_NUMBER}"
                sh "docker push localhost:5000/webappimage:${BUILD_NUMBER}"

                }
            }
            stage('Deploy to Docker'){
                steps{
                    input message: "Approve the Deploy?"
                    sh 'docker rm -f webapp'
                    sh "docker run -d -p 8095:8080 --name webapp localhost:5000/webappimage:${BUILD_NUMBER}"
                }
            }

            stage('Deploy to Kubernetes'){
                steps{
                    input message: "Deploying to k8?"
                    sh "kubectl apply -f hello-deployment.yaml"
                    sh 'sleep 5'
                    sh 'kubectl set image deployments/myapp-deployment java-app=localhost:5000/webappimage:${BUILD_NUMBER}'
                    sh 'sleep 5'
                    sh 'kubectl apply -f hello-services.yaml'
                }
            }
        }

}
