node {
  try {
     def response = httpRequest url: 'https://github.com/Gerakakliwe/jenkins-test'
     println("Status: "+response.status)
     println("Content: "+response.content)
  }
  catch(e) {
    throw e
  }
}
