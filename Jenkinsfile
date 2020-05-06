pipeline {
    agent any
    stages {
      stage('Lint HTML') {
        steps {
          sh 'cd blue && tidy -q -e *.html'
        }
		}
  
    }
}