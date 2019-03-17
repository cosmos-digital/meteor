pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'printenv'
        sh 'echo $GIT_BRANCH'
        sh 'echo $GIT_COMMIT'
        echo 'Install non-dev composer packages and test a symfony cache clear'
        sh 'ls'
        sh 'echo ${PWD}'
        sh 'docker-compose up -d'
        echo 'Building the docker images with the current git commit'
      }
    }
    stage('PHP') {
      steps {
        echo 'Composer... ${DIR_ROOT}'
        sh 'cd ./api/php/www && composer install --ignore-platform-reqs --no-scripts'
        git(url: 'https://github.com/cosmos-digital/meteor-api.git', branch: 'master', changelog: true)
        input(message: 'Choice what branch of API should builded', id: 'BRANCH_API', ok: 'Next', submitter: 'text', submitterParameter: 'BRANCH_API')
      }
    }
    stage('Test') {
      steps {
        echo 'PHP Unit tests'
        sh 'sleep 5'
      }
    }
    stage('Push') {
      agent any
      steps {
        echo 'Deploying application'
        git(url: 'https://github.com/cosmos-digital/meteor.git', branch: 'jenkins', changelog: true, poll: true)
      }
    }
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