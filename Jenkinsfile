node {

   def mvnHome

   stage('Git checkout') { // for display purposes

      // Get some code from a GitHub repository

      git 'https://github.com/GayathriDevops/hello-world-1'

      // Get the Maven tool.

      // ** NOTE: This 'M3' Maven tool must be configured

      // **       in the global configuration.          

 

       mvnHome = tool 'MVN_HOME'

   }

   

    stage('Code Analysis') {

      // Run the maven build

      withEnv(["MVN_HOME=$mvnHome"]) {

         if (isUnix()) {

            sh '"$MVN_HOME/bin/mvn" -Dmaven.test.failure.ignore clean package sonar:sonar'

         } else {

            bat(/"%MVN_HOME%\bin\mvn" -Dmaven.test.failure.ignore clean package/)

         }

      }

   } 

 

   stage('Build') {

      // Run the maven build

      withEnv(["MVN_HOME=$mvnHome"]) {

         if (isUnix()) {

            sh '"$MVN_HOME/bin/mvn" -Dmaven.test.failure.ignore clean package'

         } else {

            bat(/"%MVN_HOME%\bin\mvn" -Dmaven.test.failure.ignore clean package/)

         }

      }

   }

    stage('Nexus') {

      // Run the maven build

      withEnv(["MVN_HOME=$mvnHome"]) {

         if (isUnix()) {

            sh '"$MVN_HOME/bin/mvn" -Dmaven.test.failure.ignore clean deploy'

         } else {

            bat(/"%MVN_HOME%\bin\mvn" -Dmaven.test.failure.ignore clean package/)

         }

      }

   }

       stage('Tomcat') {

      // Run the maven build

   deploy adapters: [tomcat9(credentialsId: 'tomcat', path: '', url: 'http://13.126.95.107:8090')], contextPath: 'Gayathiri', war: '**/*.war'
     }

}
