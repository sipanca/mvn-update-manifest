pipeline {
    agent any 

    stages{
        stage ('Update Repo Github'){
            steps {
                script {
                    git branch: 'main',
                    credentialsId: 'Github-Connection',
                    url: 'https://github.com/war3wolf/mvn-update-manifest.git'  
                    
                    sh "git config user.email panca.simanjuntak@asliri.id"
                    sh "git config user.name pancaaa"
                    sh "cat deployment.yaml"
                    sh "sed -i 's+development+${DOCKERTAG}+g' deployment.yaml"
                    sh "cat deployment.yaml"
                    sh "git add ."
                    sh "git commit -m 'Done by Jenkins Job update manifest: ${env.BUILD_NUMBER}'"
                    sh "git push --set-upstream origin main"
                    sh "git push"  

                    // catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    // //withCredentials([gitUsernamePassword(credentialsId: 'github', gitToolName: 'Default')]) {
   
                    //     withCredentials([usernamePassword(credentialsId: 'Github-Connection', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                    //         sh "git config user.email panca.simanjuntak@asliri.id"
                    //         sh "git config user.name pancaaa"
                    //         sh "sed -i 's+development+${DOCKERTAG}+g' deployment.yaml"
                    //         sh "cat deployment.yaml"
                    //         sh "git add ."
                    //         sh "git commit -m 'Done by Jenkins Job update manifest: ${env.BUILD_NUMBER}'"
                    //         sh "git push --force https://github.com/war3wolf/mvn-update-manifest.git HEAD:main"
                    //     }
                    // }
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