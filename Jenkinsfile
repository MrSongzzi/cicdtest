pipeline {
  agent any
  stages {
    stage('git scm update') {
      steps {
        git url: 'https://github.com/MrSongzzi/testjenkins.git', branch: 'master'
      }
    }
    stage('docker build and push') {
      steps {
        sh '''
        sudo docker build -t newverka/testweb:newnewmain .
        sudo docker push newverka/testweb:newnewmain
        '''
      }
    }
    stage('deploy k8s') {
      steps {
        sh '''
	sudo klogin
        sudo kubectl set image deploy deploy-main ctn-main=newverka/testweb:newnewmain
        '''
      }
    }
  }
}
