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
     stage('Build Docker Image') {
            steps {
                sh 'chmod +x ./blue/run_docker.sh'
                sh 'chmod +x ./green/run_docker.sh'
                sh ' ./blue/run_docker.sh'
                sh ' ./green/run_docker.sh'
            }
        }

    }
}