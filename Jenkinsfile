pipeline{
    agent any
    stages{
        stage('clone'){
            steps{
                sh 'echo "clone"'
                sh 'unamer -r'
            }
        }
        stage('test'){
            steps{
                sh 'echo "test"'
            }
        }
        stage('createfile'){
            steps{
                sh 'touch text-$BUILD_ID'
            }
        }
    
    }
}