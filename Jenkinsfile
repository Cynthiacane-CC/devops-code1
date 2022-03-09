pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "M2_HOME"
    }

    stages {
        stage('Build with Maven') {
            steps {
                
               echo "Building the code from GIT with maven tool"
                // Get some code from a GitHub repository
                git branch: 'main', url: 'https://github.com/Cynthiacane-CC/devops-code1.git'

                // Run Maven on a Unix agent.
                sh "mvn clean package"

                // To run Maven on a Windows agent, use
                // bat "mvn -Dmaven.test.failure.ignore=true clean package"
            }
        }
        stage ('Test') {
          steps {
            echo "test step"
             sh 'mvn test'
              }

          }

        stage('Deploy to tomcat') {
            steps {
                deploy adapters: [tomcat8(credentialsId: 'TomcatUserID', path: '', url: 'http://44.202.242.138:8080/')], contextPath: null, war: '**/*.war'
                          }
        }
            // post {
            //     // If Maven was able to run the tests, even if some of the test
            //     // failed, record the test results and archive the jar file.
            //     success {
            //         junit '**/target/surefire-reports/TEST-*.xml'
            //         archiveArtifacts 'target/*.war'
            //     }
            }
        
    //}
}

