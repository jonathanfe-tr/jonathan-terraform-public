pipeline {
    agent any
    parameters {
        string(name: 'ENVIRONMENT', defaultValue: 'staging', description: 'Please choose environment dude5')
    }

    environment {
        ARM_USE_MSI = 'true'
        ARM_SUBSCRIPTION_ID = '0df0b217-e303-4931-bcbf-af4fe070d1ac'
        ARM_TENANT_ID = '812aea3a-56f9-4dcb-81f3-83e61357076e'
    }

    stages {
        stage('Init') {
            steps {
                sh """ terraform init """
            }
        }
        stage('Validate') {
            steps {
                sh """ terraform validate """
            }
        }
        stage('Plan ') {
            steps {
                sh """ terraform plan --var-file ${params.ENVIRONMENT}.tfvars -out=plan.log """
            }
        }
        stage('Plan Approval ') {
            steps {
                script {
                    if (params.ENVIRONMENT == "production") {
                       input "Deploy to prod?"
                    }
                    else if (${GIT_BRANCH} == "master") { echo 'branch is ${GIT_BRANCH}' 
                       input "Deploy to prod (branch is master)?" 
                    } 
                    else {
                        echo 'Deploying to staging'
                    }
                }
            }
        }
        stage('Notification') {
            steps {
               googlechatnotification (
                   url: "https://chat.googleapis.com/v1/spaces/AAAA2NbUb4k/messages?key=AIzaSyDdI0hCZtE6vySjMm-WEfRq3CPzqKqqsHI&token=tYGq6_ogK2LZiMq2s2oGIG4_2yB9STC_lxrG7eSSc68%3D",
                   message: 'Asafius',
                   sameThreadNotification: true,
                   suppressInfoLoggers: true
               )
            }
        }
    }
}