pipeline {
    agent {
        docker { image 'node:14-alpine' }
    }
    parameters { 
        string(name: 'ITERATION', defaultValue: '1', description: 'How many times you want to run')
        string(name: 'ENDPOINT', defaultValue: '', description: 'soap connector endpoint')
    }
    stages {
        stage('Clone the repo') {
            steps {
                git branch: 'master', url: 'git@bitbucket.org:phizzle/testing.git'
            }
        }
        stage('Run SoapConnector Postman Collection') {
            steps {
                sh """
                npm install -g newman &&
                cd soap-connector &&
                newman run soapconnector.postmancollection.json -e soapconnector.postman_environment.json -n ${ITERATION} --env-var "soapConnectorUrl=${ENDPOINT}"
                """
            }
        }
    }
}
