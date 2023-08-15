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
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') 
                     {
                        //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        //sh "git switch master"
                        sh "cat deployment.yaml"
                        sh "sed -i 's+raj80dockerid/test.*+raj80dockerid/test:${DOCKERTAG}+g' deployment.yaml"
                        sh "cat deployment.yaml"
      }
    
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



