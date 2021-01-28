pipeline {
    agent any

    stages {
        stage("Prep Workspace") {
            steps {
                prepWorkspace()
            }
        }

        stage("Build App") {
            steps {
                // This step should not normally be used in your script. Consult the inline help for details.
                withDockerContainer(image: 'maven:3.5.0-jdk-8-alpine', toolName: 'Docker') {
                    sh'mvn package'
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