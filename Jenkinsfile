pipeline {
    agent { 
        label 'java-slave'
    }
    stages {
        stage('Build') { 
            steps {
                sh 'mvn clean install' 
            }
        }
    }
}