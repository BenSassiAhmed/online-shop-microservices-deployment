pipeline{
    agent any
    stages{
        stage("Deploy to EKS"){
            environment {
                AWS_ACCESS_KEY_ID = credentials ('jenkins_aws_access_key_id')
                AWS_SECRET_ACCESS_KEY = credentials ('jenkins_aws_secret_access_key')
                AWS_SESSION_TOKEN = credentials('jenkins_aws_session_token')
            }
            steps{
                script {
                    sh "kubectl get nodes"
                    sh "chmod +x install.sh"
                    sh "./install.sh"
                    sh "helm ls"
                    sh "kubectl get deploy,svc"
                    sh "kubectl get pod"
                }
                
            }
        }
    }
}