node {
    
    def mavenHome = tool name:'3.9.10';
    
    stage('CodeCheckout'){
        git credentialsId: 'c949b28e-6278-4baf-8557-dcc7505b2790', url: 'https://github.com/NapaAravind/jenkinsPractice.git'
    }
    
    stage('Build'){
        sh "${mavenHome}/bin/mvn clean install"
    }
    
     stage('SonarCheck'){
        sh "${mavenHome}/bin/mvn sonar:sonar"
    }
    
     stage('NexoRepo'){
        sh "${mavenHome}/bin/mvn clean deploy"
    }
    
    stage('DeployAppIntoTomcat'){
        sshagent(['f92e990a-0a44-4e98-9cc5-934e32168cdc']) {
            sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@13.60.209.146:/opt/apache-tomcat-9.0.107/webapps/"
        }
    }
    
    
    
    // stage('SonarChecks'){
    //     sh "${mavenHome}/bin/mvn sonar:sonar"
    // }
}
