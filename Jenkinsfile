pipeline {
    agent any 

    stages{
        stage ('Update Repo Github'){
            steps {
                script {                   
                    def gitCreds = credentials('Github-Connection')
                    sh "git config user.email panca.simanjuntak@asliri.id"
                    sh "git config user.name war3wolf"
                    sh "cat deployment.yaml"
                    sh "sed -i 's+development+${DOCKERTAG}+g' deployment.yaml"
                    sh "cat deployment.yaml"
                    sh "git add ."
                    sh "git commit -m 'Done by Jenkins Job update manifest: ${env.BUILD_NUMBER}'"
                    sh "git push" 
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