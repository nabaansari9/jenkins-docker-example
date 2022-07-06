pipeline {
    agent any
    stages {
        stage('Git checkout') { 
            steps {
                echo 'Checking out the application'
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'GitHub_Cred', url: 'https://github.com/nabaansari9/jenkins-docker-example.git']]])
                }
                 
            }
        }
}
