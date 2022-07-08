pipeline {
    agent any
    options {
        buildDiscarder(logRotator(numToKeepStr: '5'))
    }
    environment {
        CI = true
        ARTIFACTORY_ACCESS_TOKEN = credentials('artifactory-access-token')
    }
    stages {
        stage('Build') {
            steps {
                echo 'kavoiwo'
            }
        }
        stage('Upload to artifactory') {
            agent {
                any {
                    image 'releases-docker.jfrog.io/jfrog/jfrog-cli-v2:2.2.0'
                    reuseNode true
                }
            }
            steps {
                sh 'jfrog rt upload --url http://localhost:8082/ui/artifactory/ --access-token ${ARTIFACTORY_ACCESS_TOKEN} test.txt jenkins-test/'
            }
        }
    }
}
