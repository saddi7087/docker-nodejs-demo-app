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
                
                aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 330753592456.dkr.ecr.us-east-1.amazonaws.com
                docker tag hello-softrams:latest 330753592456.dkr.ecr.us-east-1.amazonaws.com/demo-app:latest
				docker push 330753592456.dkr.ecr.us-east-1.amazonaws.com/demo-app:latest
            
                 """
                
            }
        }
        stage('Deloy Image to ECR') {
            steps {
               sh """
			      aws ecs update-service --cluster demo-app --force-new-deployment --service demo-hw
			   """
            }
        }
    }
}
