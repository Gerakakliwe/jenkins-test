pipeline {
    agent any
    environment {
        def response = httpRequest "https://www.google.com/"
        }
        stages {
            stage('get'){
                steps {
                    script {
                        echo "${response}"
			echo response.status
                        echo response.content
                    }
                }
            }
        }
    }
