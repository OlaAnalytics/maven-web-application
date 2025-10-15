node {
    try {
        // Notify build started
        sendNotifications('STARTED')

        def mavenHome = tool name: "maven3.8.6"
        echo "The Job name is: ${env.JOB_NAME}"

        stage('CheckoutCode') {
            git branch: 'development', url: 'https://github.com/OlaAnalytics/maven-web-application.git'
        }

        stage('Build') {
            sh "${mavenHome}/bin/mvn clean package"
        }
/*
        stage('ExecuteSonarQubeReport') {
            sh "${mavenHome}/bin/mvn sonar:sonar"
        }

        stage('UploadArtifactsIntoNexus') {
            sh "${mavenHome}/bin/mvn deploy"
        }

        stage('DeployAppIntoTomcatServer') {
            sshagent(['2530d036-4232-4bd1-a5ff-8f1b805f16c4']) {
                sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@16.16.124.80:/opt/apache-tomcat-9.0.97/webapps/"
            }
        }
*/
        // If no exception till here, mark success
        currentBuild.result = 'SUCCESS'

    } catch (e) {
        // Mark as failed and rethrow
        currentBuild.result = "FAILURE"
        throw e

    } finally {
        // Always send final status
        sendNotifications(currentBuild.result)
    }
}

def sendNotifications(String buildStatus = 'STARTED') {
    // Default to SUCCESS if buildStatus is null
    buildStatus = buildStatus ?: 'SUCCESS'

    // Define default values
    def colorCode = '#FF0000' // red by default

    if (buildStatus == 'STARTED') {
        colorCode = '#FFFF00' // yellow
    } else if (buildStatus == 'SUCCESS') {
        colorCode = '#00FF00' // green
    }

    def subject = "${buildStatus}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'"
    def summary = """${subject}
Job Name: ${env.JOB_NAME}
Build Number: ${currentBuild.displayName}
Build URL: ${env.BUILD_URL}
"""

    // Send notification to Slack
    slackSend(color: colorCode, message: summary)
}
