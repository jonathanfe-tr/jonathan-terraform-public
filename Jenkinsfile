pipeline {
    agent any
    parameters {
        string(name: 'ENVIRONMENT', defaultValue: 'staging', description: 'Please choose environment dude')
    }

    environment {
        ARM_USE_MSI = 'true'
        ARM_SUBSCRIPTION_ID = '0df0b217-e303-4931-bcbf-af4fe070d1ac'
        ARM_TENANT_ID = '812aea3a-56f9-4dcb-81f3-83e61357076e'
    }

    stages {
        stage('Init') {
            steps {
                sh "terraform init"
            }
        }
        stage('Validate') {
            steps {
                sh "terraform validate"
            }
        }
        stage('Plan ') {
            steps {
                sh """ terraform plan --var-file ${params.ENVIRONMENT}.tfvars -out=plan.log """
            }
        }
        stage('Plan Approval ') {
            steps {
                /* groovylint-disable-next-line LineLength */
                sh """ if ${params.ENVIRONMENT} == "staging"; then; terraform -auto-approve ${params.ENVIRONMENT}.tfvars; fi"""
            }
        }
    }
}


