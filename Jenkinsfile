pipeline{

  agent any

  stages{

      stage("Maven Build"){

        steps{

            sh "mvn -B -DskipTests clean package"

            sh "mv target/*.war target/myweb.war"

             }

            }

      stage("deploy"){

       steps{

         deploy adapters: [tomcat9(credentialsId: 'tomcat', path: '', url: 'http://13.214.155.191:8080/')], contextPath: 'Java app', war: '**/*.war'          

          }

        }

      }

    }
