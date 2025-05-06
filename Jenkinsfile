node {
def mavenHome = tool "maven-3.9.8"
// Git checkout

stage('git checkout')
{
 git branch: 'development', credentialsId: '19989165-0c03-41a1-a9b3-fdb6f603110c', url: 'https://github.com/shekardevopsaws/maven-web-application.git'

}

// Build the source code

/* Now jenkins has to connect with maven to build the source code ,we have installed maven in jenkins ----->manage jenkins--tools-maven version .Hence i have decleared the variable as mavenHome=tool name: "maven 3.9.8" */


stage('Build')
{
 sh "${mavenHome}/bin/mvn clean package"

}

// scan the source code using sonarqube

stage('scan sourcecode')
{
    sh "${mavenHome}/bin/mvn clean package sonar:sonar"
}



//push the artifacts to nexus 

stage('upload artifact into nexus')
{
    sh "${mavenHome}/bin/mvn clean package sonar:sonar deploy"
}


// Deploy to tomcat
// stage('Deploy WAR via SCP') {
//     sshagent(['tomcat-ssh']) {
//         sh """
//             scp /var/lib/jenkins/workspace/kk-funda-war-project/target/maven-web-application.war \
//             ec2-user@54.227.148.11:/opt/tomcat/webapps/
//         """
//     }
// }

stage('Deploy to Tomcat') {
        echo "Deploying WAR file using curl..."

        sh """
            curl -u mamatha:mamatha123 \
            --upload-file //var/lib/jenkins/workspace/kk-funda-war-project/target/maven-web-application.war\
            "http://54.227.148.11:8080/manager/text/deploy?path=/maven-web-application&update=true"
        """
    }


}