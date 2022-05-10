pipeline {
    agent any
    
    stages {
        stage("Get info") {
            steps {
		def response = httpRequest 'https://resttesttest.com/'
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
