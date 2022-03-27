pipeline {
    agent any
    
    tools
    {
       maven "maven-3.8.5"
    }
     
    stages {
      stage('checkout') {
           steps {
             
                git branch: 'master', url: 'https://github.com/saran-devops/CI-usingAnsible.git'
             
          }
        }
         stage('Tools Init') {
            steps {
                script {
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
               def tfHome = tool name: 'ansible'
                env.PATH = "${tfHome}:${env.PATH}"
                 sh 'ansible --version'
                    
            }
            }
        }
     
        
         stage('Execute Maven') {
           steps {
             
                sh 'mvn package'             
          }
        }
        
        
         
        
        
        
        stage('Ansible Deploy') {
             
            steps {
                 
             
               
               sh "ansible-playbook main.yml -i inventories/dev/hosts --user ansadmin --key-file /home/ansadmin/.ssh/id_rsa"

               
            
            }
        }
    }
}
