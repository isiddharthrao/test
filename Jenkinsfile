pipeline {
    agent any
    stages {
        stage('Clone') {
            steps {
                //
                echo "Cloning git repo"
                checkout([$class: 'GitSCM', branches: [[name: '$GIT_TAG']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/isiddharthrao/test.git']]])
            }
        }
        stage('Test') {
            steps {
                //
                echo "Testing"
                sh 'pwd'
                sh "ls -tlrh"
                sh 'cat index.html'
            }
        }
        stage('Deploy') {
            steps {
                //
                echo "Deploying"
                script {
                    //def remoteServer = '10.10.25.36'
                    def remoteDir = '/var/www/html'
                    //def sshKey = credentials('YOUR_SSH_CREDENTIAL_ID') // Use Jenkins credentials to store SSH private key
                    //sh "scp -i ${sshKey} -r * ${remoteServer}:${remoteDir}" // Copy files using SCP
                    sh "scp -i -r * ec2-user@${REMOTE_SERVER}:${remoteDir}" // Copy files using SCP
                }

            }
        }
    }
}
