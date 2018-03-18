pipeline {
  agent none
  stages {
    stage('build_Image_on_Dev') {
      agent{
        docker {
          image 'akash/ansible:latest'
        }
      }
      when {
        branch 'dev'
      }
      steps{
        sh "echo 'deploy the docker image'"
        sh "pip install docker-py"
        sh "ansible-playbook master.yaml"
        }
      }

    stage('on_master'){
      agent any
      when {
        branch 'master'
      }
    steps{
      sh "echo 'deploy the docker image'"
      sh "docker run -d -p 8888:80 localhost:5000/akash/testimage:v1 -name localcontainer"
      }
    }
    stage('test'){
      agent any
      when {
        branch 'master'
      }
    steps{
      sh "echo 'deploy the docker image'"
      sh "curl -I http://localcontainer:8888 > test.txt"
      sh "cat test.txt"
      }
    }
    }
  }
