pipeline {
    agent any
    
    stages {
       stage ('Clone') {
          steps {
                checkout scm
            }
        }

    stage('Update GIT') {
            steps {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')])
                    
                     {
                        //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        //sh "git switch master"
                        sh "git config user.email azeh123tanket@gmail.com"
                        sh "git config user.name bacayoco"
                        sh "cat deployment.yaml"
                        sh "sed -i 's+raj80dockerid/test.*+raj80dockerid/test:${DOCKERTAG}+g' deployment.yaml"
                        sh "cat deployment.yaml"
                         sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                         sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/updatemanifest.git HEAD:main"
      }
                }
  }
}

// https://github.com/bacayoco/updatemanifest.git
    }
    
//     post {
//         always {
//             junit 'target/surefire-reports/TEST-*.xml'
//             deleteDir()
//         }
//     }
}



