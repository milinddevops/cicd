pipeline {
    agent any
    tools {
        maven 'maven'
        jdk 'jdk8'
    }

    stages {
        stage("Init") {
            steps {
                sh'''
                echo $PATH
                '''
            }
        }

        stage("Prep Workspace") {
            steps {
                prepWorkspace()
            }
        }

        stage("Build App") {
            steps {
                sh'cd $WORKSPACE/pet-clinic; mvn clean package'
            }
        }

        stage("Build Image") {
            steps{
                sh'Building docker image ...'
            }
        }
    }
}

def prepWorkspace() {
  extWorkspace = exwsAllocate 'DiskPool'

  exws (extWorkspace) {
    checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[ url: 'https://github.com/milinddevops/cicd.git']]])

  }
}