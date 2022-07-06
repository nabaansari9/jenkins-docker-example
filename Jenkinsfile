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
        stage('SonarQube Scan'){
            steps{
                withSonarQubeEnv('SonarCloud'){
                    sh 'mvn sonar:sonar \
    			    -Dsonar.organization=nabaansari9 \
    			    -Dsonar.projectKey=jenkins-docker-example'
                }
            steps {
              timeout(time: 1, unit: 'HOURS') {
                waitForQualityGate abortPipeline: true
              }
            }
        }
    }
   }       
}
