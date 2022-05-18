pipeline{
    agent any
    stages{
        stage("Git Clone"){
            steps{
                echo "========Git Clone========"
                git branch: 'main', credentialsId: 'GitHub_Credentials', url: 'https://github.com/itsbharatsaini/jmeter.git'
                powershell 'dir'
            }   
        }

        stage("K8s Deploy"){
            steps{
                echo "========Deploy to K8s========"
                script {
                    withCredentials([kubeconfigFile(credentialsId: 'K8S_Credential', variable: 'KUBECONFIG')])
                    {

                        powershell 'kubectl apply -f Kubernetes\\jmeter-deployment.yaml'
                    }
                }
            }
        }
    }
}