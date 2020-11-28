node('node1')
{
properties([[$class: 'JiraProjectProperty'], buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5')), [$class: 'JobLocalConfiguration', changeReasonComment: ''], pipelineTriggers([pollSCM('* * * * *')])])
def mavenHome = tool name: "Maven 3.6.3"

stage('CheckoutCode')
{
git branch: 'development', credentialsId: 'e7c56d51-76eb-4dde-aa6f-1c78f38c2b4f', url: 'https://github.com/naveenkumar0989/maven-web-application.git'
}
stage('Build')
{
sh "${mavenHome}/bin/mvn clean package"
}
stage('ExecuteSonarQubeReport')
{
sh "${mavenHome}/bin/mvn sonar:sonar"
}
stage('UploadArtifactIntoNexus')
{
configFileProvider([configFile(fileId: '87e403b7-3a7b-4cfc-9309-97fd81eff6fa', targetLocation: '/home/ec2-user/node1/tools/hudson.tasks.Maven_MavenInstallation/Maven_3.6.3/conf', variable: 'nexus')])
{
sh "${mavenHome}/bin/mvn deploy"
}
}
stage('DeployAppIntoTomcatServer')
{
    sshagent(['96147af2-fc83-4967-9acd-d10b709d9425'])

{
sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@15.206.149.54:/opt/apache-tomcat-9.0.39/webapps/"
}
}

}
