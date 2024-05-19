pipeline {
    agent any

    stages {
        stage('build-docker-image') {
            steps{
                build_docker_image()
            }
        }
        stage('unit-tests') {
            steps{
                run_unit_tests()
            }
        }
        stage('deploy-dev') {
            steps {
                deploy("DEV")
            }
        }
        stage('api-test-dev') {
            steps {
                run_api_tests("DEV")
            }
        }
        stage('deploy-stg') {
            steps {
                deploy("STG")
            }
        }
        stage('api-test-stg') {
            steps {
                run_api_tests("STG")
            }
        }
        stage('deploy-prd') {
            steps {
                deploy("PRD")
            }
        }
        stage('api-test-prd') {
            steps {
                run_api_tests("PRD")
            }
        }
    }
}


def build_docker_image() {
    echo "Build sample-book-app.. "
    sh 'ls'
    sh 'docker build --no-cache -t stepanssotskovs/sample-book-app:latest .'
    sh 'docker push stepanssotskovs/sample-book-app:latest'
}

def run_unit_tests() {
    echo "Running unit tests for node application in docker container"
}

def deploy(String environment){
    echo "Deployment triggered to ${environment} environemnt.. "
}

def run_api_tests(String environment){
   echo "API Tests triggered against ${environment} environemnt.. "
}

// Build of application;
//  deployment in “DEV” env;
// Test execution against DEV env;
//  deployment in “STG” env;
// Test execution against STG env;
//  deployment in “PRD” env;
// Test execution against PRD env.
