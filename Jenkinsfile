node {
  try {
    stage('Checkout') {
      checkout scm
    }
    stage('Environment') {
      sh 'git --version'
      echo "Branch: ${env.BRANCH_NAME}"
      sh 'docker -v'
      sh 'printenv'
    }
    stage('Build Docker test'){
      sh 'docker build -t react-test -f Dockerfile.test --no-cache . '
    }
    stage('Clean Docker test'){
      sh 'docker rmi react-test'
    }
    stage('Deploy'){
      if(env.BRANCH_NAME == 'master'){
        sh 'docker build -t react-app --no-cache .'
        sh 'docker tag 192.168.99.114:8082/repository/maven-public/react-app'
        sh 'docker push 192.168.99.114:8082/repository/maven-public/react-app'
        sh 'docker rmi -f react-app 192.168.99.114:8082/repository/maven-public/react-app'
      }
    }
  }
  catch (err) {
    throw err
  }
}
