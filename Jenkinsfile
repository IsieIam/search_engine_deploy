pipeline {
  agent any
    environment{
        DeployDir = './charts/search-engine/'
        NameSpace = 'aznamespace'
        appdomain = '84.201.173.11.nip.io'
        KUBECONFIG = '/var/lib/jenkins/.kube/kubeconfig'
    }
    stages {
        stage('prepare helm') {
            steps {
                script{
                    sh '''
                          cd ${DeployDir}
                          helm dep update
                       '''
                }
            }
        }
        stage('deploy test') {
            steps {
                sh '''
                      cd ${DeployDir}
                      helm ls
                      //helm uninstall search-engine-test -n ${NameSpace}
                      helm upgrade --install search-engine-test . -f values.yaml -n ${NameSpace}
                   '''
            }
        }
        stage('test for test') {
            steps {
                sh 'curl search-engine-test.${appdomain}'
            }
        }
        stage('deploy prod') {
            steps {
                sh '''
                      cd ${DeployDir}
                      //helm uninstall search-engine-prod -n ${NameSpace}
                      helm upgrade --install search-engine-prod . -f values.yaml -n ${NameSpace}
                   '''
            }
        }
        stage('test for prod') {
            steps {
                sh 'curl search-engine-prod.${appdomain}'
            }
        }
    }
}
