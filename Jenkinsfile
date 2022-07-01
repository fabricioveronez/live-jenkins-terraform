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
                resource_group_name = credentials('resource_group_name')
                storage_account_name = credentials('storage_account_name')
                container_name = credentials('container_name')
                key = credentials('key')
            }
            steps {
                
                script {
                    dir('src') {
                        sh 'terraform init --backend-config "resource_group_name=${resource_group_name}" --backend-config "storage_account_name=${liveterraformfv}" --backend-config "container_name=${container_name}" --backend-config "key=${key}"'
                    }
                }
            }
        }

    }

}