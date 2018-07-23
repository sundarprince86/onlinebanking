node {
   stage ('Banking_Build') {   
    checkout scm
    sh 'mvn clean package -DskipTests=True'
  }
   stage ('Banking_CodeAnalysis') {
    sh 'mvn sonar:sonar -Dmaven.test.failure.ignore=true -DskipTests=true -Dsonar.sources=src/main/java'
   }

   stage ('Banking_NexusUpload') {
    sh 'mvn deploy:deploy-file -DgroupId=com.devops -DartifactId=onlinebanking -Dversion=0.2-SNAPSHOT -DgeneratePom=true -Dpackaging=war -Dfile=target/onlinebanking.war'
   } 
  
  
   stage ('Banking_tomcatDeployment') {
    sh 'mvn -P tomcatDeployment tomcat7:redeploy -DskipTests'
   }   
}     
