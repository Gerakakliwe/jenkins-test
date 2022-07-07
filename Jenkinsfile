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
rtDownload (
    serverId: 'Artifactory-1',
    spec: '''{
          "files": [
            {
              "pattern": "bazinga-repo/froggy-files/",
              "target": "bazinga/"
            }
          ]
    }''',
 
    // Optional - Associate the downloaded files with the following custom build name and build number,
    // as build dependencies.
    // If not set, the files will be associated with the default build name and build number (i.e the
    // the Jenkins job name and number).
    buildName: 'holyFrog',
    buildNumber: '42',
)
