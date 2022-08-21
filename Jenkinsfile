node {
    def app

    stage('Clone Listing API repository') {
      

        checkout scm
    }

    stage('Update  Listing API GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'jenkinsgithub', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        sh "git config user.email devsahamerlin@gmail.com"
                        sh "git config user.name devsahamerlin"
                        //sh "git switch master"
                        sh "cat deployment.yaml"
                        sh "sed 's+devsahamerlin/listingrestapi.*+devsahamerlin/listingrestapi:${DOCKERTAG}+g' deployment.yaml"
                        sh "cat deployment.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/listingapikubernetesmanifest.git HEAD:main"
      }
    }
  }
}
}
