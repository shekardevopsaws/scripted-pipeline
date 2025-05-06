node {
def mavenHome = tool name: "maven 3.9.8"
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





}