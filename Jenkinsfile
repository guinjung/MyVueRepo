pipeline {
    agent any
    environment {
        S3_BUCKET = 'vue-website-99'
        AWS_DEFAULT_REGION = 'ap-northeast-2'
    }
    stages {
        stage('Checkout') {
            steps {
                git credentialsId: 'github-token', url: 'https://github.com/guinjung/MyVueRepo.git', branch: 'main'             }
        }
        stage('Install & Build') {
            steps {
                nodejs(nodeJSInstallationName: 'node22') {
                    sh 'npm install'                     
	        sh 'npm run build'
                }
            }         
}
stage('Deploy to S3') {
            steps {
                sh "aws s3 sync ./dist s3://${S3_BUCKET} --delete"             }
        }
    }
    post {
        success {
            echo 'S3 배포  완료!'         }
        failure {
            echo '빌드  실패'         }
    } 
}

