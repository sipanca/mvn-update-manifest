pipeline {
    agent any 
 
    stages {
        stage ('Update Repo Github'){
            steps {
                script {                   
                    sshagent(credentials: ['jenkins-connection']){
                        sh '''
                        #!/bin/bash
                        # git config --global user.email 
                        # git config --global user.name 
                        cat deployment.yaml
                        sed -i "s+development+${DOCKERTAG}+g" deployment.yaml
                        cat deployment.yaml
                        git add .
                        git commit -m 'Done by Jenkins Job update manifest:${env.BUILD_NUMBER}'
                        git push origin HEAD:development        
                    '''
                    }
                    
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
