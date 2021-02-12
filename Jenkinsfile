node{
    def mavenHome = tool name: "maven3.6.3"
    stage('CheckoutCode'){
    
        git branch: 'development', url: 'https://github.com/naveenkumar0989/maven-web-application.git'
    }
    stage('Build') {
        sh "${mavenHome}/bin/mvn clean package"
    }
    stage('ExecuteSonrQubeReport'){
        sh "${mavenHome}/bin/mvn sonar:sonar"
    }
    stage('UploadAriticatsintoNexus'){
        sh "${mavenHome}/bin/mvn clean deploy"
    }
    stage('DeploymentAppIntoTomcatServer')
    {
        sshagent(['6387a875-64b8-45a9-81d5-48054856091b']) {
    sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@65.0.182.219:/opt/apache-tomcat-9.0.43/webapps/"
}
    }
}
