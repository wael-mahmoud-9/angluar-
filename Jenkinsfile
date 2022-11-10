pipeline 
{
  agent any 
  stages{
    stage ('Pull') {
      steps {
        script{
          checkout([$class: 'GitSCM', branches :[[name: '*/master']],
              userRemoteConfigs :[[
                  credentialsId : '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',
                  url : 'https://github.com/wael-mahmoud-9/angluar-.git']]])
        }
      }
    }
    stage ('Build'){
      steps{
        script{
         sh "npm install"
         sh "ansible-playbook Ansible/build.yml -i /Ansible/inventory/host.yml -e 'ansible_become_password=ansible' -vvv"
        }
      }
    }
    stage ('docker'){
      steps{
        script{
        sh "ansible-playbook ansible/docker.yml  -i ansible/inventory/host.yml -e 'ansible_become_password=ansible'"
        }
      }
    }
  }
}
