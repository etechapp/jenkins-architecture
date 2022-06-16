pipeline {
    agent {
        label {
            label 'slave1'
        }
    }
    stages {
        stage ('1-Git-Clone') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'GitHubCredentials', url: 'https://github.com/etechapp/jenkins-architecture.git']]])
            } 
        }
        stage ('2-Build-Parallel-Jobs') {
            parallel {
                stage ('slave1-sub-job-1') {
                    steps {
                        sh 'lscpu'
                        sh 'uptime'
                    }
                }
                stage ('slave1-sub-job-2') {
                    steps {
                        sh 'pwd'
                        sh 'ps -ef'
                    }
                }
            }
        }

        stage ('3-Test'){
            agent {
              label {
                label 'slave2'
              }  
            }
            steps {
                 sh 'java -version'
                echo 'Hello World'
            }
        }

        stage ('4-Deploy'){
            agent {
                label {
                    label 'slave3'
                }
            }
            steps {
                sh 'free -g'
                echo 'We Love DevOps'
            }
        }
    }
}
