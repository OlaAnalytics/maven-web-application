node
{
    
def mavenHome = tool name: "maven3.8.6"
echo "The Job name is: ${env.JOB_NAME}"
stage ('CheckoutCode'){
git branch: 'development', url: 'https://github.com/OlaAnalytics/maven-web-application.git'
}

stage('Build'){
sh "${mavenHome}/bin/mvn clean package"
}
}
/*
stage('ExecuteSonarQubeReport'){
	sh "${mavenHome}/bin/mvn sonar:sonar"
}

stage('UploadArtifactsIntoNexus'){
	sh "${mavenHome}/bin/mvn deploy"
}

stage('DeployAppIntoTomcatServer'){
sshagent(['2530d036-4232-4bd1-a5ff-8f1b805f16c4']) {
    sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@16.16.124.80:/opt/apache-tomcat-9.0.97/webapps/"
}
}

}
*/
