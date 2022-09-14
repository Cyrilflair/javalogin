pipeline{
  agent any
  stages{
		stage("Maven Build"){
        steps{
            sh "mvn -B -DskipTests clean package"
            sh "mv target/*.war target/myweb.war"
             }
            }
		stage("Docker Build"){
		steps{
			script{
				app = docker.build("app:${env.BUILD_NUMBER}")
                }
             }
          }
		stage("Docker Push"){
		steps{
			script{
				docker.withRegistry('https://083986437940.dkr.ecr.ap-southeast-1.amazonaws.com', 'ecr:ap-southeast-1:aws-root') {
				app.push("${env.BUILD_NUMBER}")
				}
			 }
		  }
		  }
		  }
}
		  
