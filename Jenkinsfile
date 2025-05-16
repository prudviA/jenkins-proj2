pipeline {
   agent any


   environment {
        IAMGE_NAME = "nodejs-cicd"
        CONTAINER_NAME = "nodejs-cicd-container"
}

stages {
   stage('clone repo') {
   	steps {
         git 'https://github.com/prudviA/jenkins-project2.git'	   
}

stage('Install Dependencies') {
	steps {
	sh 'npm install'
     }
}

   stage ('run test') {
      steps {
           sh 'npm test'
      }
}
stage('build Docker Image') {
 steps {
     sh "docker build -t $IMAGE_NAME ."
   }
}
 stage('remove old container') {
   steps {
        sh "docker rm -f $CONTAINER_NAME || true"
    }
}

  stage('Run new Container') {
     steps {
       sh "docker run -d -p 3000:3000 --name $CONTAINER_NAME $IMAGE_NAME"     }
   } 
}
post {
  success {
  echo 'Deployment successful'
}

failure {
   echo "build failure"
   }
 }
}

