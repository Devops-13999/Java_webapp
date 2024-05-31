 pipeline{
     agent any
     tools{
        maven 'MAVEN'
        jdk 'JDK'
     }
     stages{
         stage("Test"){
             steps{
                script{
                   sh 'mvn test'
               }
            }
        }
        stage("Build"){
             steps{
                script{
                   sh 'mvn clean install -DskipTests'
               }
            }
        }
     }
 }
 
