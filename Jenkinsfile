pipeline {
    agent any
    
    stages {
       stage ('Clone') {
          steps {
                checkout scm
            }
        }

    stage('Update GIT') {
            script {
                       //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                       // sh "git config user.email raj@cloudwithraj.com"
                       // sh "git config user.name RajSaha"
                        //sh "git switch master"
                        sh "cat deployment.yaml"
                        sh "sed -i 's+raj80dockerid/test.*+raj80dockerid/test:${DOCKERTAG}+g' deployment.yaml"
                        sh "cat deployment.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/kubernetesmanifest.git HEAD:main"
      }
    }


    }
    
    post {
        always {
            junit 'target/surefire-reports/TEST-*.xml'
            deleteDir()
        }
    }
}
