pipeline {
    agent any 
 
    stages {
        stage('Checkout') {
            steps {
                // Checkout your GitHub repository
                script {
                    def gitCreds = credentials('Github-Connection')
                    checkout([$class: 'GitSCM', branches: [[name: 'main']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: gitCreds, url: 'https://github.com/war3wolf/mvn-update-manifest.git']]])
                }
            }
        }

        stage ('Update Repo Github'){
            steps {
                script {                   
                    def gitCreds = credentials('Github-Connection')
                    sh '''
                        #!/bin/bash
                        git config --global user.email panca.simanjuntak@asliri.id
                        git config --global user.name war3wolf
                        cat deployment.yaml
                        sed -i "s+development+${DOCKERTAG}+g" deployment.yaml
                        cat deployment.yaml
                        git add .
                        git commit -m 'Done by Jenkins Job update manifest:${env.BUILD_NUMBER}'
                        git push origin HEAD:main        
                    '''
                }
            }
        }
    }

    post {
        always {
            deleteDir()
        }

        success {
            echo "Update Manifest Success"
        }

        failure {
            echo "Update Manifest failed"
        }

        cleanup {
            echo "Clean up in post workspace"
            cleanWs()
        }
    }
}