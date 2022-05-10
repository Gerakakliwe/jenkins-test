pipeline {
    agent any
    
    stages {
        stage("Get info") {
            steps {
		def response = httpRequest 'http://localhost:8080/jenkins/api/json?pretty=true'
		println("Status: "+response.status)
		println("Content: "+response.content)
            }
        }
        stage ("Parsing") {
            steps {
                echo "Yeehoo"
            }
        }
    }
}
