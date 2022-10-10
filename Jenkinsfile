pipeline{
    //Directives
    agent any
    tools {
        maven 'maven'
    }

    environment{
        ArtifactId = readMavenPom().getArtifactId()
       Version = readMavenPom().getVersion()
       Name = readMavenPom().getName()
       GroupId = readMavenPom().getGroupId()
        
    }

    stages {
        // Specify various stage with in stages

        // stage 1. Build
        stage ('Build'){
            steps {
                sh 'mvn clean install package'
            }
        }

        // Stage2 : Testing
        stage ('Test'){
            steps {
                echo ' testing......'

            }
        }

        // Stage3  Deploying
       /* stage('Deploy'){
            steps{
                echo 'deplying....'
            }
        }*/

        // Stage3 : Publish the source code to Sonarqube
       /* stage ('Sonarqube Analysis'){
            steps {
                echo ' Source code published to Sonarqube for SCA......'
                withSonarQubeEnv('sonarqube'){ // You can override the credential to be used
                     sh 'mvn sonar:sonar'
                }

            }
        }*/
        //Stage3 : Publish the source code to nexus
        stage ('Sonarqube Analysis'){
            steps {
                nexusArtifactUploader artifacts: [[
                    artifactId: 'VinayDevOpsLab',
                     classifier: '', file: 'target/VinayDevOpsLab-0.0.10-SNAPSHOT.war',
                      type: 'war']], 
                      credentialsId: '3c801841-b07c-4746-9226-a1db343f7347', 
                      groupId: 'com.vinaysdevopslab', 
                      nexusUrl: '18.116.44.114:8081', 
                      nexusVersion: 'nexus3', 
                      protocol: 'http', 
                      repository: 'RohitDevOpsLab-SNAPSHOT', 
                      version: '0.0.10-SNAPSHOT'
                }

            }

            //Stage 4 : Print some information
            stage('Pring Environmnet Variable'){
            steps{
                echo "Artifact ID is ....'${ArtifactId}'"
                echo "Version is '${Version}'"
                echo "GroupID is '${GroupId}'"
                echo "Name is '${Name}'"
            }
        }

        

         // Stage5  Deploying
       stage('Deploy'){
            steps{
                echo 'deplying....'
            }
        }

        
        
    }

}