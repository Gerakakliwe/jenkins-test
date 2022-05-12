node {
    // Ensure WS is clean before we start
    deleteDir()
    // Checkout GIT
    def git_info = checkout scm
    def error
    try {
    stage("Get changelog") {
    def changeLogSets = currentBuild.changeSets
    def changeLog = []
        for (int i = 0; i < changeLogSets.size(); i++) {
            def entries = changeLogSets[i].items
            for (int j = 0; j < entries.length; j++) {
                def entry = entries[j]
                changeLog.add([commit_msg:"${entry.msg}", commit_hash:"${entry.commitId}"])
                //echo "Commit id: ${entry.commitId}, \n Commit author: ${entry.author} \n Commit date: ${new Date(entry.timestamp)} \n Commit message: ${entry.msg}"
            }
        }
        changeLog.groupBy { 
            if (it.msg =~ /op-\d*/)
                (it.msg =~ /op-\d+/).findAll()
            else
                "no ticket :("
        }.each { entry ->
            println(entry.key)
            entry.value.each {
                println('\t' + it.msg)
            }
        }
}
    } catch(e) {
        error = e
        throw e
    }
}

@NonCPS
def getSorted(def toBeSorted){
    toBeSorted.sort{ it.commit_msg }
}

@NonCPS
def groupBy(def toBeGrouped){
    toBeGrouped.groupBy{ it[1] }.collectEntries{ k, v -> [(k):v*.get(0)] }
}

@NonCPS
def ifCommentHasTicket(def commitMessage){
    if (commitMessage.contains("OP-")){
        println(commitMessage + " has a jira ticket")
    } else {
        println(commitMessage + " DOESN'T HAVE")
    }
}
