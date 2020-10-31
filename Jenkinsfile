pipeline {
  agent any
    environment{
        DeployDir = './charts/search-engine/'
        NameSpace = 'aznamespace'
    }
    stages {
        stage('prepare') {
            steps {
                script{
                    //TODO - add modify of image tag in helm values
                    //TODO - add custom external ingress ip-address
                    cd ${DeployDir}
                    sh 'helm dep update'
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
                sh 'curl search-engine-test.ipaddress.nio.io'
            }
        }
        stage('deploy prod') {
            steps {
                sh 'helm install search-engine-prod -n ${NameSpace}'
            }
        }
        stage('test for prod') {
            steps {
                sh 'curl search-engine-prod.ipaddress.nio.io'
            }
        }
    }
}
