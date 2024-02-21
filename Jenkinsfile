pipeline {
    agent { 
        label 'kube-slave'
    }
    stages {
        stage('Build') { 
            agent {
                docker {
                    image 'docker.io/maven:3.8.6'
                }
            }
            steps {
                sh 'mvn clean install' 
            }
        }
        stage('Test') {
            steps {
                // Since no specific agent is defined, it will reuse the previous node/container
                script {
                    currentBuild.rawBuild.environments.get("JENKINS_NODE_COOKIE") // Forces the same node/container to be reused
                }
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Deliver') {
            steps {
                // Since no specific agent is defined, it will reuse the previous node/container
                script {
                    currentBuild.rawBuild.environments.get("JENKINS_NODE_COOKIE") // Forces the same node/container to be reused
                }
                sh './jenkins/scripts/deliver.sh'
            }
        }
    }
}

