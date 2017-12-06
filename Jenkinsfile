node {
   def mvnHome
   stage('Preparation') {
     checkout scm 
   }
   stage('Build') {
      sh 'docker run -i --rm --name my-maven-project -v "$PWD":/usr/src/mymaven -w /usr/src/mymaven maven:3-jdk-8 mvn clean package'
   }
   stage('Javadoc') {
      sh 'docker run -i --rm --name my-maven-project -v "$PWD":/usr/src/mymaven -w /usr/src/mymaven maven:3-jdk-8 mvn site'
   }
   stage('Results') {
      junit '**/target/surefire-reports/TEST-*.xml'
      echo "Archiving target files:"
      sh 'ls target/*.jar'
      archive 'target/*.jar'
   }
}
