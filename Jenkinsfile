node {
    stage('Update GIT') {
        script {
            catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                withCredentials([sshUserPrivateKey(credentialsId: "github-ssh", keyFileVariable: 'key')]) {
                    git url: "git@github.com:Davi-Coelho/subathon-countdown-web-manifest.git",
                        credentialsId: 'github-ssh',
                        branch: 'main'
                    sh "git config user.email davi.cmbarreto@gmail.com"
                    sh "git config user.name Davi-Coelho"
                    sh "cat deployment.yaml"
                    sh "sed -i 's+registry.davicoelho.com/subathon-timer/timer.*+registry.davicoelho.com/subathon-timer/timer:${TAG}+g' deployment.yaml"
                    sh "cat deployment.yaml"
                    sh "git add ."
                    sh "git commit -m 'Done by Jenkins Job subathontimer-build: ${env.BUILD_NUMBER}'"
                    sh 'git push origin main'
                }
            }
        }
    }
}
