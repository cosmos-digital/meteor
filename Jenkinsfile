pipeline {
    agent { docker { image 'cosmosdigital/php-v7' } }
    stages {
        stage('build') {
            steps {
                sh 'php --version'
            }
        }
    }
}
