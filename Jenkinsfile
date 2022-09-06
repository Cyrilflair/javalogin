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

          deploy adapters: [tomcat9(credentialsId: 'admintomcat', path: '', url: 'http://18.142.122.80:8080')], contextPath: null, war: '**/*.war'          

          }

        }

      }

    }
