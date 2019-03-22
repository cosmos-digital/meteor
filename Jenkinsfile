pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        sh 'echo ${PWD}'
        sh 'echo ${JOB_NAME}'
        sh 'ls'
      }
    }
    stage('API'){
      steps {
        dir('./data/php/api') {
          sh 'git clone https://github.com/cosmos-digital/meteor-api.git www'
          dir('./www') {
            sh 'git checkout master && git pull'
            sh 'docker run --rm --interactive --tty  --volume $PWD:/app  composer install --ignore-platform-reqs --no-scripts'
            sh 'ls'
          }
        }
      }
    }
    stage('Deploy'){
      steps{
        stash name: 'docker-stash', includes: '**'
        dir('/data/meteor') {
          unstash 'docker-stash'
          sh 'docker-compose up -d'
        }
      }
    }
  }
  post { 
    always { 
      cleanWs()
    }
  }
}