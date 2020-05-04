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
    }
}
