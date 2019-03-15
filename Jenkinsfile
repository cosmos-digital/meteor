pipeline {
  agent any
  stages {
    stage('test_write') {
      steps {
        writeFile(file: 'test.txt', text: 'testeee', encoding: 'utf8')
      }
    }
    stage('test_print') {
      steps {
        echo 'testandooo'
      }
    }
  }
}