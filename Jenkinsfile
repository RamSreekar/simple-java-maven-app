pipeline {
  agent {
    label 'java-slave'
  }
  stages {
    stage('Build') {
        steps {
            container('java-maven') {
                sh 'mvn -B -DskipTests clean package'
            }
        } 
    }

    stage('Test') {
        steps {
            container('java-maven') {
                sh 'mvn test'
                post {
                    always {
                        junit 'target/surefire-reports/*.xml'
                    }
                }
            }
        }
    }

    stage('Deliver') {
        steps {
            container('java-maven') {
                sh './jenkins/scripts/deliver.sh'
            }
        } 
    }
  }
}