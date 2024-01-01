pipeline {
  environment {
    vm_ip = "192.168.56.10"
    private_key = '/home/sahil/Learn/dev-ops/vagrant/.vagrant/machines/default/virtualbox/private_key'
  }
  agent any
  stages {
    stage('Moving application resources to VM') {
      steps {
          sh '''#!/bin/bash
              echo "private_key: ${private_key}"
              echo "vm_ip: ${vm_ip}"
              cat ${private_key}
              # scp -i ${private_key} -r ./public vagrant@${vm_ip}:/home/vagrant/app/
              # scp -i ${private_key} ./index.js vagrant@${vm_ip}:/home/vagrant/app/
              # scp -i ${private_key} -r ./package.json vagrant@${vm_ip}:/home/vagrant/app/
              # scp -i ${private_key} ./.env vagrant@${vm_ip}:/home/vagrant/app/
          '''
      }
    }
    stage('SSHing into VM') {
      steps{
        sh '''#!/bin/bash
              ssh -i ${private_key} vagrant@${vm_ip}
              cd ~/app/
          '''
      }
    }
    stage('Installing dependencies') {
      steps{
        sh '''#!/bin/bash
              rm -fR node_modules
              npm install
          '''
      }
    }
    stage('Starting Application') {
      steps{
        sh '''#!/bin/bash
              npm start >> logs.txt & && exit
          '''
      }
    }
  }
}
