pipeline {
    agent any
    
    def build_image

    properties([buildDiscarder(logRotator(numToKeepStr: "5"))])

    // Ensure WS is clean before we start
    deleteDir()

    checkout scm
    
    stages {
        stage('Build Image') {
            agent {
                docker { image "enrichments" }
                reuseNode true
            }
        }
        stage("Unit Test") {
            slackSend(message:"ABOUT TO FAIL")
            error("TEST ERROR")
            sh "python3.7 --version"
            sh "virtualenv --python=/usr/bin/python3.7 venv3 && . venv3/bin/activate && pip3 install --no-cache-dir -r requirements.txt && ./run-jenkins-tests.sh"
            def results = findFiles(glob: "systempackages/**/test_output.xml")
            def result_paths = ""
            results.each { item ->
                result_paths = result_paths + " " + "${item.path}"
            }
            sh "xunitmerge ${result_paths} results_combined.xml"
            junit "results_combined.xml"
        }
        stage("Code Quality") {
            def metadata_list = findFiles(glob: "systempackages/**/metadata.json")
            metadata_list.each { item ->
                def metadata_path = "${item.path}"
                def path_only = metadata_path.substring(0, metadata_path.lastIndexOf("/"))

                // Only run on python3 enrichments
                def status_code = sh script: "cd ${path_only} && grep -c is_python3 metadata.json", returnStatus:true
                if (status_code == 0) {
                    def enrichment_name = path_only.substring(path_only.lastIndexOf("/") + 1, path_only.length())
                    sh ". venv3/bin/activate && cd ${path_only} && PYTHONPATH=source:${WORKSPACE}/sdkdeliverables/enrichment_sdk_3.0/contents/anomali_enrichment_sdk_3.0/lib/:${WORKSPACE}/venv3/lib/python3.7/site-packages/ pylint --rcfile=${WORKSPACE}/.pylintrc --output-format=parseable --reports=no --exit-zero source > pylint.log"
                    echo "Recording issues for: metadata_path=${metadata_path} path_only=${path_only} enrichment_name=${enrichment_name} name=\"Pylint - ${enrichment_name}\" pattern=\"${path_only}/pylint.log\""
                    recordIssues enabledForFailure: true, qualityGates: [[threshold: 1, type: "TOTAL_HIGH", unstable: true]], tools: [pyLint(id: "pylint-${enrichment_name}", name: "Pylint - ${enrichment_name}", pattern: "${path_only}/pylint.log")]
                } else {
                    echo "Skipping ${path_only} as it has not been converted to Python3"
                }
            }
        }
    }
}


//         }
//     }
//     post {
//         failure {
//             slackSend(message:"FAILURE")
//         }
//     }
// }
