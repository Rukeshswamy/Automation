pipeline {
    agent {
        docker { image 'node:14-alpine' }
    }
    parameters { 
        string(name: 'ENV', defaultValue: 'Dev', description: '')
        string(name: 'DEVICE_ID', defaultValue: '3', description: '')
        choice(name: 'DEVICE_NAME', choices: ['metone', 'climet', 'aerotrack', 'lasair'], description: 'Select Device Type') 
        string(name: 'SLEEP_AFTER_SAMPLE', defaultValue: '10', description: '')
        string(name: 'PHARMA_API', defaultValue: 'http://a8c07b02785d54dfc9d2c657083c1932-1789001200.us-east-2.elb.amazonaws.com', description: '')
        string(name: 'ACTION_MANAGER', defaultValue: 'http://a8986eaaf9a2047ac8d46065124805ad-1667697664.us-east-2.elb.amazonaws.com', description: '')
        string(name: 'DB_HOST', defaultValue: 'a1a5301589d3d439298ca53d7d920d89-2090013161.us-east-1.elb.amazonaws.com', description: '')
        string(name: 'DB_NAME', defaultValue: 'merck', description: '')
        string(name: 'DB_USER', defaultValue: 'pharmaapi', description: '')
        string(name: 'DB_PASSWORD', defaultValue: 'NJgU6h4YywMYauBG', description: '')
        string(name: 'DB_PORT', defaultValue: '5432', description: '')
        string(name: 'HEARTBEATAPI', defaultValue: 'http://localhost:9090/heartbeat/merck_pharma_heartbeat', description: '')
    }
    stages {
        stage('Clone the repo') {
            steps {
                git branch: 'master', url: 'git@bitbucket.org:phizzle/testing.git'
            }
        }
        stage('Run External Samples Test Automation') {
            steps {
                sh """
                apk update &&
                apk add python3 make gcc g++ &&
                cd disconnect &&
                npm install &&
                export ENV=${ENV} &&
                export DEVICE_ID=${DEVICE_ID} &&
                export DEVICE_NAME=${DEVICE_NAME} &&
                export SLEEP_AFTER_SAMPLE=${SLEEP_AFTER_SAMPLE} &&
                export PHARMA_API=${PHARMA_API} &&
                export ACTION_MANAGER=${ACTION_MANAGER} &&
                export DB_HOST=${DB_HOST} &&
                export DB_NAME=${DB_NAME} &&
                export DB_USER=${DB_USER} &&
                export DB_PASSWORD=${DB_PASSWORD} &&
                export DB_PORT=${DB_PORT} &&
                export HEARTBEATAPI=${HEARTBEATAPI} &&
                npm run external_samples_tests
                """
            }
        }
    }
}