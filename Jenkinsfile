stages {
    stage('Scan Code') {
      steps{
        withSonarQubeEnv('sonarqube') {
          sh "mvn sonar:sonar"
        }
      }
    }
    
    stage('Build') {
      steps {
        sh '"mvn" -Dmaven.test.failure.ignore clean install'
      }
    }
    stage('Test') {
      steps {
        sh '"mvn" -Dmaven.test.failure.ignore test'
      }
      post {
        always{
          junit '**/target/surefire-reports/TEST-*.xml'
        }
      }
    }
}
