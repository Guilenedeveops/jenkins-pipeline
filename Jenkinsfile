pipeline{
    agent any
    stages{
        stage('codescan'){
            steps{
                sh 'trivy fs . -o result.html'
                sh 'cat result.html'
                
            }
        }
        stage('dockerLogin'){
            steps{
                sh 'aws ecr get-login-password --region us-east-1 |\
                 docker login --username AWS\
                 --password-stdin 867344455679.dkr.ecr.us-east-1.amazonaws.com'
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
                sh 'docker tag jenkins-ci-not-to-be-delete:latest\
                867344455679.dkr.ecr.us-east-1.amazonaws.com/jenkins-ci-not-to-be-delete:latest'
                sh 'docker tag jenkins-ci-not-to-be-delete:latest 867344455679.dkr.ecr.us-east-1.amazonaws.com/jenkins-ci-not-to-be-delete:v1.$BUILD_NUMBER'
            }
        }
       

        stage('pushImage'){
            steps{
                sh 'docker push 867344455679.dkr.ecr.us-east-1.amazonaws.com/jenkins-ci-not-to-be-delete:latest'
                sh 'docker push 867344455679.dkr.ecr.us-east-1.amazonaws.com/jenkins-ci-not-to-be-delete:v1.$BUILD_NUMBER'
            }
        }
    
    }
}