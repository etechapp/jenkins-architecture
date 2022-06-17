pipeline {
    agent {
        label {
            label 'slave1'
        }
    }
    stages {
        stage ('0-Git-Clone') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'GitHubCredentials', url: 'https://github.com/etechapp/jenkins-architecture.git']]])
            } 
        }
        stage ('1-slave1-Parallel-Jobs') {
            parallel {
                stage ('slave1-sub-job-1') {
                    steps {
                        sh 'lscpu'
                        sh 'uptime'
                    }
                }
                stage ('slave1-sub-job-2') {
                    steps {
                        sh 'ls -i'
                        sh 'ls -a'
                    }
                }
            }
        }

        stage ('2-slave2-Test'){
            agent {
              label {
                label 'slave2'
              }
            } 
              steps {
                sh 'ls'
              } 
        }
            stage ('slave2-stage-1') {
                steps {
                    sh 'java --version'
                    echo 'Hello World'
                }
            }
            stage ('slave2-stage-2') {
                steps {
                    sh 'free -g'
                }
            }       
        stage ('3-slave3-Deploy'){
            agent {
                label {
                    label 'slave3'
                }
            }
           steps {
             sh 'ls'
            }
        }
            stage ('slave3-stage-1') {
                steps {
                    sh 'ps -ef'
                }
            }
            stage ('slave3-stage-2') {
                steps {
                    echo 'The Wonderful Team EtechApp'
                    echo 'We love DevOps'
                }
            }
        }
    }
