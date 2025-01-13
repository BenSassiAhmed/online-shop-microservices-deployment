pipeline{
    agent any
    stages{
        stage("A"){
            steps{
                script {
                    sh "kubectl get nodes"
                    sh "kubectl create -f k8s-config/config-basic.yaml"
                    sh "sleep 15"
                    sh "kubectl get deploy,svc"
                }
                
            }
        }
    }
}