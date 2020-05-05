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
        stage ('Lint html') {
            steps {
                sh 'tidy -q -e *.html'
            }
        }
        stage ('QC Testing') {
            when {
                branch 'staging'
            }
            steps {
                echo '"Deploy build to staging env. for testing by QC."'
            }
        }
        stage ('Deploy to Green') {
            when {
                brnach 'Green'
            }
            steps {
                sh '"Deploying to Green Producion"'
                withAWS(credentials:'jenkins-aws') {
                    s3Upload(pathStyleAccessEnabled: true, payloadSigningEnabled: true, file:'index.html', bucket:'app.mrdevops.uk/green')
                }
            }
        }
        stage ('Route traffic to Green Deployment') {
            when {
                brnach 'Green'
            }
            input {
                message "Do you want to route all production's traffic to Green site?"
                ok "Yes, Confirmed."
                submitter "mahmoudrashwan"
            }
            steps {

                sh '"Users traffic Routing to Green Producion site."'
            }
        
        }
    }
}
