pipeline {
    agent any
    tools {
        maven 'Maven' 
    }
    stages {
        stage('Git checkout') { 
            steps {
                echo 'Checking out the application'
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'GitHub_Cred', url: 'https://github.com/nabaansari9/jenkins-docker-example.git']]])
                }
                 
            }
        stage('Build') {
            steps{
                sh 'mvn clean install'
            }    
        }
       /* stage('SonarQube Scan'){
            steps{
                withSonarQubeEnv('SonarCloud'){
                    sh 'mvn sonar:sonar \
    			    -Dsonar.organization=nabaansari9 \
    			    -Dsonar.projectKey=jenkins-docker-example'
                }
        } */
        stage("Publish to Nexus Repository Manager") {
            steps {
                nexusArtifactUploader artifacts: [
                    [
                        artifactId: 'my-app', 
                        classifier: '', 
                        file: 'target/Hello World 1.0-SNAPSHOT.jar', 
                        type: 'jar'
                        ]
                    ], 
                    credentialsId: 'NEXUS_CRED', 
                    groupId: 'com.mycompany.app', 
                    nexusUrl: 'http://18.205.22.131:8081', 
                    nexusVersion: 'nexus3', 
                    protocol: 'http', 
                    repository: 'maven-central-repository', 
                    version: '1.0-SNAPSHOT'

            }
    }
   }     
