pipeline{

  agent any

  stages{

      stage("Scan"){

        steps{

         withSonarQubeEnv('sonarqube') {

         sh "mvn clean package sonar:sonar"

         }

        }

      }

      stage("Build"){

        steps{

            sh '"mvn" -Dmaven.test.failure.ignore clean install'

             }

            }

      stage('Test') {

        steps {

          sh 'mvn test'

      }

      post {

        always {

            junit '**/target/surefire-reports/TEST-*.xml'

             }

           }

      }
      stage("deploy"){
       steps{
          deploy adapters: [tomcat9(credentialsId: 'admin', path: '', url: 'http://13.212.169.36:8080/')], contextPath: null, war: '**/*.war'          
          }
        }
      }
    }
