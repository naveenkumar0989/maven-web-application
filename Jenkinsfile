node{
    def mavenHome = tool name: "maven3.6.3"
    stage('checkoutcode'){
        git branch: 'development13feb', url: 'https://github.com/naveenkumar0989/maven-web-application.git'
        
    }
    stage('build'){
        sh "${mavenHome}/bin/mvn clean package"
        
    }
    stage('verify the code'){
        sh "${mavenHome}/bin/mvn sonar:sonar"
    }
    stage('Upload to code nexus'){
        sh "${mavenHome}/bin/mvn clean deploy"
    }
    stage('deploy into apache'){
        
    }
}
