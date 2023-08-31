pipeline {
    agent any 

    stages{
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
                        git commit -m "Done by Jenkins Job update manifest:${env.BUILD_NUMBER}"
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
            echo "Build image Success"
        }

        failure {
            echo "Build image failed"
        }

        cleanup {
            echo "Clean up in post workspace"
            cleanWs()
        }
    }
}