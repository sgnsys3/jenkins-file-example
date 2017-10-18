pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        sh 'echo "Build Step"'
        sh 'echo wow > index.html'
        slackSend channel: '#devops', color: 'good', message: "[${JOB_NAME}] เริ่มการ Build แล้ว อิอิ จุ๊กกรู๊ - ${BUILD_NUMBER}", teamDomain: 'alchemist-itbangmod'
      }
    }
    stage('unit-test') {
      steps {
        sh 'echo "Running Unit Test"'
      }
    }
    stage('zipfile') {
      steps {
        sh 'echo ${JOB_NAME}-${BUILD_NUMBER}'
        sh 'tar cvzf "${JOB_NAME}-${BUILD_NUMBER}.tar.gz" *'
      }
    }
    stage('development') {
      steps {
        sh 'echo "Deploy To Development"'
        sh 'scp "${JOB_NAME}-${BUILD_NUMBER}.tar.gz" deployment@helloworld.itbangmod.in.th:/jenkins-artifact/Testing-PIPELINE/'
      }
    }
    stage('staging') {
      steps {
        timeout(time: 30, unit: 'SECONDS') {
          input 'Deploy to Production ?'
        }
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
      slackSend channel: '#devops', color: 'good', message: "[${JOB_NAME}] Build เสร็จแล้ว - ${BUILD_NUMBER} พร้อมกับ Deploy", teamDomain: 'alchemist-itbangmod'
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
    aborted {
      echo 'Aborted'
    }
  }
}