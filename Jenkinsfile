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
                buildDockerImage()
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

def buildDockerImage() {
    withDockerRegistry(toolName: 'Docker', url: 'docker.io/milinddocker/cicd', credentialsId: 'DockerHubCredentials',) {
        dir('pet-clinic') {
            def custImage = docker.build("cicd:${env.BUILD_ID}")
            custImage.push() 
        }
    }
}
