/*pipeline {
   agent any

   stages {
     
      stage('Preparation') {
         steps {
            cleanWs()
            git 'https://github.com/pipeline-testing/ansible-pods.git'
         }
      }
      stage('Preparation1') {
         steps {
            sh 'docker images'
         }
      }

     
      stage('Run ansible'){
         agent {
            kubernetes {
               label 'promo-app'  // all your pods will be named with this prefix, followed by a unique id
               idleMinutes 30  // how long the pod will live after no jobs have run on it
               yamlFile 'build-pod.yaml'  // path to the pod definition relative to the root of our project 
             }
          }
  
          steps{
             container('ansible'){
                sh 'ansible-playbook demo.yaml'
              }
          }    
         
      }
    }
}
*/


    podTemplate(containers: [
    containerTemplate(name: 'ansible', image: 'ansible/ansible:centos7', command: 'sleep', args: '99d'),
  ]) {

    node(POD_LABEL) {
        stage('Run Ansible') {
            git 'https://github.com/pipeline-testing/ansible-pods.git'
            sh 'kubectl logs -l jenkins=slave -f '
            container('ansible') {
                stage('Run Ansible playbook') {
                    sh 'ansible-playbook demo.yaml'
                }
            }
        }


    }
}
   

