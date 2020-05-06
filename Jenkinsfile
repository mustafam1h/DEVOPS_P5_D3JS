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
                sh 'cd blue && ./run_docker.sh'

            }
        }
     stage('Build Docker Image G') {
            steps {
                sh 'cd green && ./run_docker.sh'

            }
        }
    }
}