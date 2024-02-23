podTemplate(containers: [
    containerTemplate(
        name: 'java-maven', 
        image: 'docker.io/maven:3.9.0',
        command: 'sleep', 
        args: '30d'
    )
]) {

    node(POD_LABEL) {
        stage ('Java app test') {
            branch: 'master'
            container('java-maven') {
                stage('Test maven installation') {
                    sh 'mvn -v'
                } 
                stage('Check code files') {
                    sh 'ls -al'
                }
            }
        }
    }
}