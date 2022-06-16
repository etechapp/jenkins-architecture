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

        stages ('3-Test'){
            agent {
              label {
                label 'slave2'
              }  
            }
        }
            stage ('slave2-stage-1') {
                steps {
                    sh 'java -version'
                    echo 'Hello World'
                }
            }
            stage ('slave2-stage-2') {
                steps {
                    sh 'free -g'
                    sh 'sudo systemctl status jenkins'
                }
            }

        stages ('4-Deploy'){
            agent {
                label {
                    label 'slave3'
                }
            }
            stage ('slave3-stage-1') {
                steps {
                    git branch: 'main',
                          url: "${repoUrl}"
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
}