pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                // Get some code from a GitHub repository
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/Cyrilflair/javalogin.git']]])



               sh "mvn clean install"
	       sh "mv target/*.war target/myweb.war"
            }
        
        }
        
        stage('Docker') {
            steps {
                sh "docker build -t pipeline3 ."
            }
        }
        stage('Push to ecr') {
            steps {
                script {
                    sh "aws ecr get-login-password --region ap-southeast-1 | docker login --username AWS --password-stdin 083986437940.dkr.ecr.ap-southeast-1.amazonaws.com"
                    sh "docker tag pipeline3:latest 083986437940.dkr.ecr.ap-southeast-1.amazonaws.com/pipeline3:latest"
                    sh "docker push 083986437940.dkr.ecr.ap-southeast-1.amazonaws.com/pipeline3:latest"
        }
      }
    }



       stage("Deploy to EKS"){
            steps{
                sh 'aws eks update-kubeconfig --name demo-eks --region ap-southeast-1'
              sh '/root/bin/kubectl apply -f deployment.yml'
        }
    }
  }
}
