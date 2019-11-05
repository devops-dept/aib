node('maven-label') {
   def mvnHome = tool 'M3'
   stage('Preparation') { 
      git 'https://github.com/devops-dept/aib.git'           
   }
   stage('Build') {
      withEnv(["MVN_HOME=$mvnHome"]) {
         if (isUnix()) {
            sh '"$MVN_HOME/bin/mvn" -Dmaven.test.failure.ignore clean deploy sonar:sonar -Dsonar.host.url=http://ip-172-31-29-140.us-west-1.compute.internal:9000'
         } else {
            bat(/"%MVN_HOME%\bin\mvn" -Dmaven.test.failure.ignore clean deploy/)
         }
      }
   }
   stage('Results') {
      junit '**/target/surefire-reports/TEST-*.xml'
      archiveArtifacts 'target/*.jar'
   }
}
