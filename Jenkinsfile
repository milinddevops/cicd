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

        stage("Run Ansible-Playbook") {
            steps{
                sshagent(['ssh-jenkins']) {
                    sh'ssh -o StrictHostKeyChecking=no root@10.125.214.94 "ansible-playbook /opt/play/deploy_application.yaml --extra-vars build_id=${JOB_NAME}_${BUILD_NUMBER} -i /opt/play/inventory.txt"'
                }
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
    withDockerRegistry(toolName: 'Docker', url: 'https://index.docker.io/v1/', credentialsId: 'DockerHubCredentials',) {
        dir('pet-clinic') {
            def custImage = docker.build("milinddocker/cicd:${env.BUILD_ID}")
            custImage.push() 
        }
    }
}
