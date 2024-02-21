pipeline {
    agent {
        label 'kube-slave'
    }
    stages {
        stage("docker agent") {
            agent {
                docker {
                    image 'docker.io/maven:3.8.6'
                }
            }
    
            stages {
                stage('Build') {
                    steps {
                        sh 'mvn -B -DskipTests clean package'
                    }
                }
                stage('Test') {
                    steps {
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
                        sh './jenkins/scripts/deliver.sh'
                    }
                }  
            }
        }
    }
}
