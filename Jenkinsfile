pipeline {
    agent any
    stages {
        stage ('build') {
            steps {
                sh 'echo "Build is running"'
                sh '''
                     echo "this step will compile code in real scenario"
                     ls -lah
                 '''
            }
        }
        stage ('Upload to AWS') {
            steps {
                withAWS(credentials:'jenkins-aws') {
                    s3Upload(pathStyleAccessEnabled: true, payloadSigningEnabled: true, file:'index.html', bucket:'clouddevops-project3-green')
                }
            }
        }
    }
}
