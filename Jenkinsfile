pipeline{
  agent { label '1' }
  tools{
    maven "maven3.8.6"
}
stages {
 stage('1GetCode'){
   steps{
    sh "echo 'cloning the latest application version' "
   git credentialsId: 'gitcredential', url: 'https://github.com/LandmarkDistiction/Nissan'
   }
 }
stage('2 Test and Build'){
  steps{
  sh "echo 'running Junit test cases'"
  sh "mvn clean package"
  }
}
stage('4 Code Quality'){
    steps{
       sh "echo 'performing code quality' "
       sh "mvn sonar:sonar"
    }
}
stage('5uploadNexus'){
    steps{
    sh "mvn deploy"
    }
}
stage('6 deploy2prod'){
    steps{
       deploy adapters: [tomcat9(credentialsId: 'tomcat-credentials', path: '', url: 'http://52.53.189.193:8080/')], contextPath: null, war: 'target/*war' 
    }
}
}
post{
  always{
      emailext body: '''Hey guys
Good job , build and deployment is successful

Thanks
Kehinde Ajayi
3462194117''', recipientProviders: [buildUser(), developers()], subject: 'success', to: 'honda-app@gmail.com'
}
success{
    emailext body: '''Hey guys
Good job , build and deployment is successful

Thanks
Kehinde Ajayi
3462194117''', recipientProviders: [buildUser(), developers()], subject: 'success', to: 'honda-app@gmail.com'
}
failure{
    emailext body: '''Hey guys
Build Fails

Thanks
Kehinde Ajayi
3462194117''', recipientProviders: [buildUser(), developers()], subject: 'success', to: 'honda-app@gmail.com'
  }
 }
}
