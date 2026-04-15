pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'docker build -t myapp:v2 .'
      }
    }
    stage('Deploy Green') {
      steps {
        sh 'kubectl apply -f green-dep.yaml'
      }
    }
    stage('Switch Traffic') {
      steps {
        input "Switch to Green?"
        sh '''
        kubectl patch service myapp-service \
        -p '{"spec":{"selector":{"app":"myapp","color":"green"}}}'
        '''
      }
    }
  }
}
