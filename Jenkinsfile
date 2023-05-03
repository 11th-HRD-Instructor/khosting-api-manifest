node {
    def app
    stage('Clone repository') {
        checkout scm
    }
    stage('Update GIT') {
        script {
            catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                withCredentials([usernamePassword(credentialsId: 'Jekin-Github-Token', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                    sh 'git config user.email rotanakkosal03@gmail.com'
                    sh 'git config user.name Rotanakkosal'
                    sh 'cat khosting-api-manifest/spring-api-deployment.yml'
                    sh "sed -i 's+khosting/khosting-api-v1.*+khosting/khosting-api-v1:${DOCKERTAG}+g' khosting-api-manifest/spring-api-deployment.yml"
                    sh 'git add .'
                    sh "git commit -m 'Done by Jenkins Job change manifest: ${env.BUILD_NUMBER}'"
                    sh 'git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/11th-HRD-Instructor/khosting-infra.git HEAD:main'
                    notifyEvents message: 'API Update successfully!', token: 'YCCI6mB8DHwtSlRoWGCFCT3OjPeifK5R'
                }
            }
        }
    }
}
