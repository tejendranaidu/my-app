pipeline{
    agent any
    stages{
        stage("SCM Checkout"){
            steps{
                git branch: 'master', 
                credentialsId: 'github', 
                url: 'https://github.com/jagadeesh-nani/my-app'
            }
            
        }
        stage("Maven"){
            steps{
                sh 'mvn clean package'
            }
            
        }
        stage("Nexus Artifact"){
            steps{
                script{
                    def pomFile = readMavenPom file: 'pom.xml'
                   def pomVersion = pomFile.version
                    nexusArtifactUploader artifacts: 
               [
                   [artifactId: 'myweb', classifier: '', file: "target/myweb-${pomVersion}.war", type: 'war']
                   ], 
                   credentialsId: 'nexus3', 
                   groupId: 'in.javahome', 
                   nexusUrl: '172.31.10.37:8081', 
                   nexusVersion: 'nexus3', 
                   protocol: 'http', 
                   repository: 'naniapp-release', 
                   version: pomVersion
                }
               
            }
            
        }
    }
}
