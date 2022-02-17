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
          deploy adapters: [tomcat8(credentialsId: 'TomcatUserID', path: '', url: 'http://3.86.227.86:8080/')], contextPath: null, war: '**/*.war'
         }

     }

	   
 def remote = [:]
 remote.name = "Ansible"
 remote.host = "52.207.249.13"
 remote.allowAnyHosts = true
 Ansible {
   withCredentials([usernamePassword(credentialsId: 'AnsibleUserID', passwordVariable: 'password', usernameVariable: 'userName')]) {
   remote.user = userName
   remote.password = password

   stage('Deploy_k8s') {
      steps {
         echo "deploy to Kubernetes"
      script{
	 sshCommand remote: remote, command: "ansible-playbook /etc/ansible/kube.yml"
             }
           }
       }
    }
 }   

}

