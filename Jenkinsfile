pipeline {
    agent any 
    stages {
        stage('Stage 1') {
            steps {
                echo 'Hello world!' 
            }
        }
        stage('Stage 2') {
            steps {
                echo 'Aboba world!' 
            }
        }
        stage('Stage 3') {
            steps {
                echo 'Bye world!' 
            }
        }
    }
}
rtServer (
    id: 'Artifactory-1',
    url: 'http://my-artifactory-domain/artifactory',
    // If you're using username and password:
    username: 'user',
    password: 'password',
    // If you're using Credentials ID:
    credentialsId: 'ccrreeddeennttiiaall',
    // If Jenkins is configured to use an http proxy, you can bypass the proxy when using this Artifactory server:
    bypassProxy: true,
    // Configure the connection timeout (in seconds).
    // The default value (if not configured) is 300 seconds:
    timeout: 300
)
