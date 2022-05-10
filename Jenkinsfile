node {
  try {
     def response = httpRequest 'https://github.com/Gerakakliwe/jenkins-test'
     println("Status: "+response.status)
     println("Content: "+response.content)
  }
  catch(e) {
    throw e
  }
}
