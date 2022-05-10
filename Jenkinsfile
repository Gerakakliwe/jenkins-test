pipeline {
    agent any
    
    stages {
        stage("Send notification") {
	    def response = httpRequest 'http://localhost:8080/jenkins/api/json?pretty=true'
	    println("Status: "+response.status)
	    println("Content: "+response.content)
        }
        stage ("Test One") {
            steps {
                echo "Yeehoo"
            }
        }
    }
}
