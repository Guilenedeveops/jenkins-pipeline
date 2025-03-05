pipeline{
    agent any
    stages{
        stage('codescan'){
            steps{
                sh 'trivy --version'
                
            }
        }
        stage('dockerImageBuild'){
            steps{
                sh 'docker -v'
            }
        }
        stage('pushImage'){
            steps{
                sh 'docker ps'
            }
        }
    
    }
}