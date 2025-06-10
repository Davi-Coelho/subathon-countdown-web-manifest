node {
    stage('Clone repository') {
        checkout scm
    }

    stage('Update GIT') {
        script {
            catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                sshagent (credentialsId: 'github-ssh') {
                    sh "git config user.email davi.cmbarreto@gmail.com"
                    sh "git config user.name Davi-Coelho"
                    sh "cat deployment.yaml"
                    sh "sed -i 's+registry.davicoelho.com/subathon-timer/timer.*+registry.davicoelho.com/subathon-timer/timer:${TAG}+g' deployment.yaml"
                    sh "cat deployment.yaml"
                    sh "git add ."
                    sh "git commit -m 'Done by Jenkins Job subathontimer-build: ${env.BUILD_NUMBER}'"
                    sh "git remote set-url origin git@github.com:Davi-Coelho/subathon-countdown-web-manifest.git"
                    sh "git push origin HEAD:main"
                }
            }
        }
    }
}
