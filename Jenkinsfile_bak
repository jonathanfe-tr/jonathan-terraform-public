pipeline {
    agent any
    parameters {
        string(name: 'DOCKERFILE', defaultValue: 'Dockerfiletemp', description: 'choose dockerfile...')
    }
    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                sh """
                pip3 install .
                python3 tests.py
                """
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
                sh """
                docker build -t alison . -f ${params.DOCKERFILE}
                """
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying.... dude man 5'
            }
        }
    }
}

#init
#validate
#plan +varfile
#
