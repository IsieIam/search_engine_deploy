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
                          cd ${DeployDir}
                          helm dep update
                       '''
                }
            }
        }
        stage('deploy test') {
            steps {
                //sh 'helm install search-engine-test -n ${NameSpace}'
                sh 'helm upgrade --install search-engine-test . -f values.yaml -n ${NameSpace}'
            }
        }
        stage('test for test') {
            steps {
                sh 'curl search-engine-test.${appdomain}'
            }
        }
        stage('deploy prod') {
            steps {
                sh 'helm upgrade --install search-engine-prod . -f values.yaml -n ${NameSpace}'
            }
        }
        stage('test for prod') {
            steps {
                sh 'curl search-engine-prod.${appdomain}'
            }
        }
    }
}
