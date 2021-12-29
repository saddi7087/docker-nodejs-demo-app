pipeline {
    agent any
    
    stages {
        stage('Code Build') {
            steps {
               sh """
               cd ${env.WORKSPACE}
					     pwd
					     docker build -t hello-softrams .
                """
				       }
          }

        stage('Push Image to ECR') {
            steps {
                sh """
                
                aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 014958301348.dkr.ecr.us-east-1.amazonaws.com
                docker tag hello-softrams:latest 014958301348.dkr.ecr.us-east-1.amazonaws.com/demo-app-1:latest
		docker push 014958301348.dkr.ecr.us-east-1.amazonaws.com/demo-app-1:latest
            
                 """
                
            }
        }
        stage('Deloy Image to ECR') {
            steps {
               sh """
			      aws ecs update-service --cluster demo-app-demo --force-new-deployment --service demo-hw-service-demo
			   """
            }
        }
    }
}
