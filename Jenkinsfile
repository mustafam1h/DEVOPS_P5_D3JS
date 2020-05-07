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
            
                   withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'pass', usernameVariable: 'user')]) {
    // the code in here can access $pass and $user
      sh ' cd blue && sudo chmod +x upload_docker.sh && sudo ./upload_docker.sh $pass '
           }
                 
                             
         }
     }
      stage('Push  to ECR') {
          steps {	  
        sh 'aws ecr get-login-password --region us-east-2 | docker login --username AWS --password-stdin 291671365597.dkr.ecr.us-east-2.amazonaws.com'
        sh 'cd blue && docker build -t bluegreen .'
        sh 'sudo docker tag bluegreen:latest 291671365597.dkr.ecr.us-east-2.amazonaws.com/bluegreen:latest'
        sh 'sudo docker push 291671365597.dkr.ecr.us-east-2.amazonaws.com/bluegreen:latest'
        sh 'kubectl apply -f ./blue/blue-controller.json'
        sh 'kubectl apply -f blue-green-service.json'
          }
      }  
      stage('Push  to EKS') {
          steps {	  
        withAWS(credentials: 'mustafa', region: 'us-east-2') {
          sh 'eksctl create cluster'
          sh 'sudo chmod 777 /var/lib/jenkins/.docker/config.json'
          sh 'kubectl config use-context 291671365597.dkr.ecr.us-east-2.amazonaws.com/bluegreen:latest'
          sh 'kubectl apply -f ./blue/blue-controller.json'
          sh 'kubectl apply -f blue-green-service.json'
              }
          }
      }
   }
        
}
