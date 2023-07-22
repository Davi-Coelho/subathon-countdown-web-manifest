node {
    stage('Clone repository') {
        checkout scm
    }

    stage('Update GIT') {
        script {
            catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                    sh "git config user.email davi.cmbarreto@gmail.com"
                    sh "git config user.name Davi-Coelho"
                    sh "cat deployment.yaml"
                    sh "sed -i 's+registry.davicoelho.com/subathon-timer/timer.*+registry.davicoelho.com/subathon-timer/timer:${DOCKERTAG}+g' deployment.yaml"
                    sh "cat deployment.yaml"
                    sh "git add ."
                    sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                    sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/subathon-countdown-web-manifest.git HEAD:main"
                }
            }
        }
    }
}