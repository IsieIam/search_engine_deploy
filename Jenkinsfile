pipeline {
  agent any
    environment{
        DeployDir = './charts/search-engine/'
        NameSpace = 'aznamespace'
        appdomain = '84.201.173.11.nio.io'
    }
    stages {
        stage('prepare') {
            steps {
                script{
                    //TODO - add modify of image tag in helm values
                    //TODO - add custom external ingress ip-address
                    sh '''
                          helm dep update'
                          cd ${DeployDir}
                       '''
                }
            }
        }
        stage('deploy test') {
            steps {
                sh 'helm install search-engine-test -n ${NameSpace}'
            }
        }
        stage('test for test') {
            steps {
                sh 'curl search-engine-test.${appdomain}'
            }
        }
        stage('deploy prod') {
            steps {
                sh 'helm install search-engine-prod -n ${NameSpace}'
            }
        }
        stage('test for prod') {
            steps {
                sh 'curl search-engine-prod.${appdomain}'
            }
        }
    }
}
