# PRoject 5 "Capstone DEVOPS Udacity"
## Deploy D3.JS Visualizing HTML to the covid 19 cases in blue green deployment using Jenkins CI/CD 


### The project using Jenkins as CI/CD 

Runnig the application 
<br>
1- Building the docker image using  ``` ./run_docker.sh ``` for blue and grean <br>
2-pushing the images to dockerhub.io using ``` ./upload_docker.sh ``` <br>
3- Running the kubernets cluster using ``` ./run_kuberentes.sh ``` <br>
4- To run blue deployment 
  <br> *Create a new stage to set current kubectl context to use the kubectl configuration file and info of cluser like 

5- Container deployment using EKS cluster on Fargate 
#pre-requsites 
- eksctl: Official CLI to create a new EKS cluster.
- kubectl: CLI to interact with the kubernetes API server
- AWS CLI + Docker: We will use Docker and the AWS CLI to build and push a Docker image for our application.

<br>
Jenkins Stages 

![JENKINS](1.JPG)


<br>
D3.js App is used to graph the new cases in Riyadh and Cairo of COVID 19 using wikepedia 
