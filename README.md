## Deploy D3.JS in blue green deployment using Jenkins CI/CD 


The project using Jenkins as CI/CD 

Runnig the application 

1- Building the docker image using ./run_docker.sh for blue and grean
2-pushing the images to dockerhub.io using ./upload_docker.sh
3- Running the kubernets cluster using ./run_kuberentes.sh
4- To run blue deployment 
   *Create a new stage to set current kubectl context to use the kubectl configuration file and info of cluser like 
   `aws eks --region us-east-1 update-kubeconfig --name prod`
     `kubectl config use-context arn:aws:eks:us-east-2:291671365597:cluster/prod`

Jenkins Stages 

![JENKINS](1.JPG)



D3.js App is used to graph the new cases in Riyadh and Cairo of COVID 19 using wikepedia 