pipeline {
    agent any 

    stages{
        stage ('Update Repo Github'){
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    //withCredentials([gitUsernamePassword(credentialsId: 'github', gitToolName: 'Default')]) {
   
                    withCredentials(credentialsId: 'Github-Connection') {
                        sh "sed -i 's+development+${DOCKERTAG}+g' deployment.yaml"
                        sh "cat deployment.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job update manifest: ${env.BUILD_NUMBER}'"
                        sh "git push --force https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/mvn-update-manifest.git HEAD:main"
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