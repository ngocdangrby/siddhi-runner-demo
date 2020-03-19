pipeline {
  agent any
  stages {
    stage('build docker image') {
      steps {
        sh '''#image name
NAME=\'siddhivt/siddhi-runner-test\'

#remove previous image if existed
docker image rm -f $(docker images | grep $NAME |  awk \'{print $3}\')

#build new image from Dockerfile
docker build . -t $NAME
docker login -u ngocdangrby -p D01693187796
docker push $NAME
docker ps
'''
      }
    }

    stage('Pull test code') {
      steps {
        git(url: 'https://github.com/ngocdangrby/siddhi-test-suite', branch: 'master')
        sh '''cd siddhi-test-suite
ls
mvn test'''
      }
    }

  }
}