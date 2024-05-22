pipeline {
    agent any
    triggers {
        pollSCM('*/1 * * * *')
    }

    stages {
        stage('build-docker-image') {
            steps{
                build_docker_image()
            }
        }
        stage('deploy-dev') {
            steps {
                deploy("dev")
            }
        }
        stage('api-test-dev') {
            steps {
                run_api_tests("DEV")
            }
        }
        stage('deploy-stg') {
            steps {
                deploy("stg")
            }
        }
        stage('api-test-stg') {
            steps {
                run_api_tests("STG")
            }
        }
        stage('deploy-prd') {
            steps {
                deploy("prd")
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
    echo "Building docker image.. "
    sh "docker build --no-cache -t stepanssotskovs/sample-book-app:latest ."

    echo "Running unit tests for node application in docker container.. "
    sh "docker run --rm --entrypoint=npm stepanssotskovs/sample-book-app:latest run test "

    echo "Pushing docker image to the docker registry"
    sh "docker push stepanssotskovs/sample-book-app:latest"   
}


def deploy(String environment){
    echo "Deployment triggered to ${environment} environemnt.. "
    sh "docker compose stop sample-book-app-${environment}"
    sh "docker compose rm sample-book-app-${environment}"
    sh "docker compose up -d sample-book-app-${environment}"
}

def run_api_tests(String environment){
   echo "API Tests triggered against ${environment} environemnt.. "
//    sh "docker run -v ${PWD}/api-test-report-${environment}:/api-tests/mochawesome-report --network=host --rm stepanssotskovs/api-tests run BOOKS BOOKS_${environment}"
   sh "docker run --network=host --rm stepanssotskovs/api-tests run BOOKS BOOKS_${environment}"
}

// Build of application;
//  deployment in “DEV” env;
// Test execution against DEV env;
//  deployment in “STG” env;
// Test execution against STG env;
//  deployment in “PRD” env;
// Test execution against PRD env.
