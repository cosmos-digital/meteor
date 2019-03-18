pipeline {
    agent any
    stages {
      stage('Build') {
        steps {
          cleanWs()
          sh 'printenv'
          sh 'echo $GIT_BRANCH'
          sh 'echo $GIT_COMMIT'
          sh 'echo ${PWD}'
          echo 'Building the docker images with the current git commit'
        }
      }
    stage('INSTALL COMPOSER') {
        steps{
          echo 'Deploying application'
          dir('./data/php/api/www') {
            sh 'git clone https://github.com/cosmos-digital/meteor-api.git -b test'
            sh 'ls'
            dir('./meteor-api') {
              sh 'ls'
              sh 'docker run --rm --interactive --volume $PWD:/app  composer install --ignore-platform-reqs --no-scripts'
            }
          }
        }
    }
    stage('Test') {
      steps {
        echo 'PHP Unit tests'
        sh 'sleep 5'
      }
    }
    stage('Docker'){
      steps{
        sh 'docker-compose up -d'
      }
    }
    // stage('Push') {
    //   agent any
    //   steps {
    //     echo 'Deploying application'
    //     git(url: 'https://github.com/cosmos-digital/meteor-full.git', branch: 'jenkins', changelog: true, poll: true)
    //   }
    // }
  }
  environment {
    APP_VERSION = '1'
  }
  post {
    always {
      echo 'always'

    }

  }
}