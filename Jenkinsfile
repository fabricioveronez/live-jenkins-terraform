pipeline {
    agent any

    stages {

        stage('Checkout source') {
            steps {
                git url: 'https://github.com/fabricioveronez/live-jenkins-terraform.git', branch: 'main'
            }
        }

        stage('Criação ou atualização da infra') {
            environment {
                ARM_CLIENT_ID = credentials('ARM_CLIENT_ID')
                ARM_CLIENT_SECRET = credentials('ARM_CLIENT_SECRET')
                ARM_SUBSCRIPTION_ID = credentials('ARM_SUBSCRIPTION_ID')
                ARM_TENANT_ID = credentials('ARM_TENANT_ID')
                resource_group_name = credentials('resource_group_name')
                storage_account_name = credentials('storage_account_name')
                container_name = credentials('container_name')
                az_key = credentials('az_key')
            }
            steps {
                
                script {
                    dir('src') {
                        sh 'terraform init -migrate-state --backend-config "resource_group_name=${resource_group_name}" --backend-config "storage_account_name=${storage_account_name}" --backend-config "container_name=${container_name}" --backend-config "key=${az_key}"'
                        sh 'terraform apply --auto-approve'
                    }
                }
            }
        }

    }

}
