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
                sh 'sudo apt install docker.io'
                sh 'sudo systemctl start docker'
                sh 'sudo systemctl enable docker'
                sh 'sudo usermod -aG docker ${USER}'
                sh 'sudo systemctl restart docker'
                sh 'cd blue && chmod +x run_docker.sh && sudo ./run_docker.sh'

            }
        }
     stage('Build Docker Image G') {
            steps {
                sh 'cd green && chmod +x run_docker.sh &&  ./run_docker.sh'

            }
        }
    }
}