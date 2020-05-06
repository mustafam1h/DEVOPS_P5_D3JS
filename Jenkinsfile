pipeline {
    agent any
    stages {
      stage('Lint HTML BLUE') {
        steps {
          sh 'cd blue && tidy -q -e *.html'
        }
		}
      stage('Lint HTML GREEN') {
        steps {
          sh 'cd green && tidy -q -e *.html'
        }
		}
     stage('Build Docker Image B') {
       
            steps {
              //  sh 'sudo apt install docker.io'
                //sh 'sudo systemctl start docker'
               // sh 'sudo systemctl enable docker'
               // sh 'sudo usermod -aG docker ${USER}'
               // sh 'sudo systemctl restart docker'
                sh 'cd blue && chmod +x run_docker.sh && sudo ./run_docker.sh'

            }
        }
     stage('Build Docker Image G') {
            steps {
       //         sh 'sudo apt install docker.io'
         //       sh 'sudo systemctl start docker'
           //     sh 'sudo systemctl enable docker'
             //   sh 'sudo usermod -aG docker ${USER}'
               // sh 'sudo systemctl restart docker'
                sh 'cd green && chmod +x run_docker.sh && sudo ./run_docker.sh'
            }            
        }

        stage('push Docker Container') {
      		steps {
                   
                    docker.withRegistry('', 'dockerhub') {
                    sh 'cd blue && sudo chmod +x upload_docker.sh && ./upload_docker.sh'
                    }            
             }
        }
        
        stage('Deploying to EKS') {
            steps {
                dir('k8s') {
                    withAWS(credentials: 'aws-credentials', region: 'eu-west-1') {
                            sh "eksctl create cluster --name prod --region us-east-2 --fargate"
                            sh 'kubectl apply -f ./blue-green-service.json'
                        }
                    }
            }
        }
        
    }
}