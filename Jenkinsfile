pipeline {
    // These are pre-build sections
    agent {
        node {
            label 'AGENT-1'
        }
    }
    options {
        timeout(time: 10, unit: 'MINUTES') 
        disableConcurrentBuilds()
    }
    // This is build section
    stages {
        stage('Read Version') {
            steps {
                script{
                    def packageJSON = readJSON file: 'package.json'
                    appVersion = packageJSON.version
                    echo "app version: ${appVersion}"
                }
            }
        }
        stage('Install Dependencies') {
            steps {
                script{
                    sh """
                        sudo dnf module disable nodejs -y
                        sudo dnf module enable nodejs:20 -y
                        sudo dnf install nodejs -y
                        npm install
                    """
                }
            }
        }
        stage('Build Image') {
            steps {
                script{

                          sh """
                           
                             docker build -t catalogue:${appVersion} .
                             docker images
                        

                          """ 
                }
            }
        }

    }

    post{
        always{
            echo 'I will always say Hello again!'
            cleanWs()
        }
        success {
            echo 'I will run if success'
        }
        failure {
            echo 'I will run if failure'
        }
        aborted {
            echo 'pipeline is aborted'
        }
    }
}    
