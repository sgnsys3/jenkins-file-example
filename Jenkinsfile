pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        sh 'echo "Build Step"'
        sh 'pwd'
        sh 'whoami'
        slackSend channel: '#devops', color: 'good', message: 'เริ่มการ Build แล้วคร้าบบบ', teamDomain: 'alchemist-itbangmod'
      }
    }
    stage('unit-test') {
      steps {
        sh 'echo "Running Unit Test"'
      }
    }
    stage('development') {
      steps {
        sh 'echo "Deploy To Development"'
        sh 'ssh deployment@helloworld.itbangmod.in.th cd /var/www && ls -l'
      }
    }
    stage('staging') {
      steps {
        sh 'echo "Deploy To Stagging"'
      }
    }
    stage('production') {
      steps {
        sh 'echo "Deploy To Production"'
      }
    }
  }
  post {
    always {
      echo 'This job was ended'
    }
    success {
      echo 'Success XD'
    }
    failure {
      echo 'Failure :('
    }
    unstable {
      echo 'Not OK Dude'
    }
    changed {
      echo 'This will run only if the state of the Pipeline has changed'
      echo 'For example, if the Pipeline was previously failing but is now successful'
    }
  }
}