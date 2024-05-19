pipeline {
    agent any

    stages {
        stage('build-docker-image') {
            steps{
                script {
                    build_docker_image()
                }
            }
        }
        stage('unit-tests') {
            steps{
                script {
                    run_unit_tests()
                }
            }
        }
        stage('deploy-dev') {
            steps {
                script{
                    deploy("DEV")
                }
            }
        }
        stage('api-test-dev') {
            steps {
                script{
                    run_api_tests("DEV")
                }
            }
        }
        stage('deploy-stg') {
            steps {
                script{
                    deploy("STG")
                }
            }
        }
        stage('api-test-stg') {
            steps {
                script{
                    run_api_tests("STG")
                }
            }
        }
        stage('deploy-prd') {
            steps {
                script{
                    deploy("PRD")
                }
            }
        }
        stage('api-test-prd') {
            steps {
               script{
                    run_api_tests("PRD")
                }
            }
        }
    }
}


def build_docker_image() {
    echo "Build sample-book-app.. "
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
