pipeline{

agent any

stages{

  //Getting the code from GitHub Repo
  stage('CheckoutCode'){
  steps{
  
 git branch: 'deploy', url: 'https://github.com/OlaAnalytics/maven-web-application.git'
      }
  }
  
  //After getting coe doing the build using maven
  stage('Build'){
  steps{
   sh "mvn clean package"
  }
  }
  
}//stages closing 
}//Pipeline closing
