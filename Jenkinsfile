pipeline {
  agent {
    kubernetes {
      yaml """
apiVersion: v1
kind: Pod
metadata:
  labels:
    some-label: some-label-value
spec:
  containers:
  - name: packer
    image: hashicorp/packer 
    command: 
    - bash
    tty: true
"""
    }
  }
  environment {
    CREDS = credentials('alhanouf-aws-creds')
    AWS_ACCESS_KEY_ID = "${CREDS_USR}"
    AWS_SECRET_ACCESS_KEY = "${CREDS_PSW}"
    OWNER = 'rho'
    PROJECT_NAME = 'rho-web-server'
    TOKEN=credentials('1be568b2-5054-466a-a48d-14dd2d1b9945')
  }
  stages {
      stage("build") {
          steps {
              container('packer') {
                  sh 'packer build packer.json'
              }
          }
      }
  }
}

