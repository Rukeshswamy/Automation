pipeline {
    agent {
        docker { image 'node:14-alpine' }
    }
    stages {
        stage('Clone the repo') {
            steps {
                git branch: 'master', url: 'git@bitbucket.org:phizzle/testing.git'
            }
        }
        stage('Run samples Postman Collection') {
            steps {
                sh """
                npm install -g newman &&
                cd SampleTests &&
                newman run runsamples.postman_collection.json -e Dev-env.postman_environment.json -g My_Workspace.postman_globals.json -r htmlextra --reporter-htmlextra-export report.html --bail newman
                """
            }
        }
    }
}
