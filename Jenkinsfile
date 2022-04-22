pipeline {
  agent any
  stages {
    stage('git scm update') {
      steps {
        git url: 'https://github.com/MrSongzzi/cicdtest.git', branch: 'master'
      }
    }
    stage('docker build and push') {
      steps {
        sh '''
        sudo docker build -t newverka/testweb:newnewmain .
        sudo docker push newverka/testweb:newnewmain
        sudo echo "Jenkins shop test" > index.html 
	sudo docker build -t newverka/testweb:newshop .
        sudo docker push newverka/testweb:newshop

	sudo echo "Jenkins blog test" > index.html
        sudo docker build -t newverka/testweb:newblog .
        sudo docker push newverka/testweb:newblog

	'''
      }
    }
    stage('deploy k8s') {
      steps {
        sh '''
	sudo klogin
        sudo kubectl set image deploy deploy-main ctn-main=newverka/testweb:newnewmain
	sudo kubectl set image deploy deploy-shop ctn-shop=newverka/testweb:newshop
	sudo kubectl set image deploy deploy-blog ctn-blog=newverka/testweb:newblog

        '''
      }
    }
  }
}
