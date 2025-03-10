pipeline{
    agent any
    environment{
        AWS_REGION = 'us-east-1'
        IMAGE_ECR_REPO = '867344455679.dkr.ecr.us-east-1.amazonaws.com/jenkins-ci-not-to-be-delete'
        ECR_REPO = '867344455679.dkr.ecr.us-east-1.amazonaws.com'
    }
    stages{
        stage('codescan'){
            steps{
                sh 'trivy fs . -o result.html'
                sh 'cat result.html'
                
            }
        }
        stage('dockerLogin'){
            steps{
                sh "aws ecr get-login-password --region $AWS_REGION |\
                 docker login --username AWS\
                 --password-stdin $ECR_REPO"
            }
        }
        stage('dockerImageBuild'){
            steps{
                sh 'docker build -t jenkins-ci-not-to-be-delete .'
                sh 'docker build -t imageversion .'
            }
        }
        stage('dockerImageTag'){
            steps{
                sh "docker tag jenkins-ci-not-to-be-delete:latest $IMAGE_ECR_REPO:latest"
                sh "docker tag jenkins-ci-not-to-be-delete:latest $IMAGE_ECR_REPO:v1.$BUILD_NUMBER"
            }
        }
       

        stage('pushImage'){
            steps{
                sh "docker push $IMAGE_ECR_REPO:latest"
                sh "docker push $IMAGE_ECR_REPO:v1.$BUILD_NUMBER"
            }
        }
    
    }
}