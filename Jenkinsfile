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



 stage ('Deploy') {
        steps {
          echo "deploy to tomcat"
          deploy adapters: [tomcat8(credentialsId: 'TomcatUserID', path: '', url: 'http://3.86.96.235:8080/')], contextPath: null, war: '**/*.war'
         }

     }




   }



}

