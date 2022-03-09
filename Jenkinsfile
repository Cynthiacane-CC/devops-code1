pipeline {
   agent any
   
   tools {
     maven 'M2_HOME'
     //git 'git'
     //jdk 'JAVA_HOME'

         }
   environment {
     registry = 'cynthiacane20/devops-code1'
     dockerCrdentials = 'DockerUserID'

               }
   
   stages {
     stage ('Git clone') {
        steps {
          echo 'clone GIt repo'
	  git branch: 'main', url: 'https://github.com/Cynthiacane-CC/devops-code1.git'

	          }
     
            }

	   
     stage ('Build') {
        steps {
          echo 'build step'
	  sh 'mvn clean install package' 

	          }
     
           }

 stage ('Test') {
        steps {
          echo "test step"
          sh 'mvn test'
              }

           }


 stage ('CreateImage') {
        steps {
          echo "deploy to docker registry step"
        script {
          docker.build registry + ":$BUILD_NUMBER"
	           }
	
             }

           }
 stage ('Deploy_Tomcat') {
        steps {
          echo "deploy to tomcat"
          deploy adapters: [tomcat8(credentialsId: 'TomcatUserID', path: '', url: 'http://18.212.6.210:8080/')], contextPath: null, war: '**/*.war'
         }

     }

	      
 stage ('Ansible Deploy') {
        steps {
          echo "deploy to kubernetes"
           sh "ansible-playbook kube.yml -i /etc/ansible/hosts -- user AnsibleUserID"
              } 
            }
       }   
   
   }
