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
    url: 'http://localhost:8082/ui/artifactory',
    // If you're using username and password:
    username: 'admin',
    password: 'Xthtgfirf123.',
    // Configure the connection timeout (in seconds).
    // The default value (if not configured) is 300 seconds:
    timeout: 300
)
