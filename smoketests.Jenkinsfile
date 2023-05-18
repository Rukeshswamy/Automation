pipeline {
    agent {
        docker { image 'node:14-alpine' }
    }
    parameters { 
        string(name: 'ITERATION', defaultValue: '1', description: 'How many times you want to run')
    }
    stages {
        stage('Clone the repo') {
            steps {
                git branch: 'master', url: 'git@bitbucket.org:phizzle/testing.git'
            }
        }
        stage('Run SmokeTest Postman Collection') {
            steps {
                sh """
                npm install -g newman &&
                cd smoke-tests &&
                newman run smoketests.postmancollection.json -e smoketests.postman_environment.json -n ${ITERATION}
                """
            }
        }
    }
}
