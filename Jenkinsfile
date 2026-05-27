pipeline {
  agent {
    kubernetes {
      label 'jenkins-agent-my-app'
      yaml '''
apiVersion: v1
kind: Pod
metadata:
  labels:
    component: ci
spec:
  containers:
  - name: python
    image: python:3.11.8
    command:
    - cat
    tty: true
   - name: docker
     image: docker
     command:
     - cat
     tty: true
     volumeMounts:
     - mountPath: /var/run/docker.sock
       name: docker-sock
   - name: kubectl
     image: lachlanevenson/k8s-kubectl:v1.17.2
     command:
     - cat
     tty: true
  volumes:
  - name: docker-sock
    hostPath:
      path: /var/run/docker.sock
'''
    }

<<<<<<< HEAD
     triggers {
         pollSCM('* * * * *')
     }
=======
  }
  stages {
    stage('Test python') {
      steps {
        container(name: 'python') {
          sh 'pip install -r requirements.txt'
          sh 'python test.py'
        }

      }
    }
>>>>>>> 185fcfac5f3366324d2df4bc13eec28ecf6319c9

    stage('Build image') {
      steps {
        container(name: 'docker') {
          sh 'docker build -t localhost:4000/pythontest:latest .'
          sh 'docker push localhost:4000/pythontest:latest'
        }

<<<<<<< HEAD
        // stage('Build image') {
        //     steps {
        //         container('docker') {
        //             sh "docker build -t localhost:4000/pythontest:latest ."
        //             sh "docker push localhost:4000/pythontest:latest"
        //         }
        //     }
        // }

        stage('Deploy') {
            steps {
                container('kubectl') {
                    sh "kubectl apply -f ./kubernetes/deployment.yaml"
                    sh "kubectl apply -f ./kubernetes/service.yaml"
                }
            }
        }
=======
      }
>>>>>>> 185fcfac5f3366324d2df4bc13eec28ecf6319c9
    }

    stage('Deploy') {
      steps {
        container(name: 'kubectl') {
          sh 'kubectl apply -f ./kubernetes/deployment.yaml'
          sh 'kubectl apply -f ./kubernetes/service.yaml'
        }

      }
    }

  }
  triggers {
    pollSCM('* * * * *')
  }
}