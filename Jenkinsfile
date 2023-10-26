pipeline {
  agent any

  parameters {
    booleanParam(defaultValue: false, description: 'Run the first requirement', name: 'RUN_FIRST_REQUIREMENT')
    booleanParam(defaultValue: false, description: 'Run the second requirement', name: 'RUN_SECOND_REQUIREMENT')
    booleanParam(defaultValue: false, description: 'Run the third requirement', name: 'RUN_THIRD_REQUIREMENT')
    booleanParam(defaultValue: false, description: 'Run the second script', name: 'RUN_SECOND_SCRIPT')
  }

  stages {
    stage('Requirements') {
      when {
        expression {
          params.RUN_SECOND_SCRIPT == false
        }
      }
      steps {
        script {
          if (params.RUN_FIRST_REQUIREMENT && params.RUN_SECOND_REQUIREMENT && params.RUN_THIRD_REQUIREMENT) {
            echo "All requirements PASSED, Push allowed on the next build"
          }
        }
      }
    }

    stage('Push') {
    when {
        expression {
            params.RUN_SECOND_SCRIPT == true
        }
    }
    steps {
        script {
          
            // If there are changes, commit and push them
            //if (sh(returnStatus: true, script: 'git diff --exit-code') != 0) {
                sh 'git add .'
                sh "git commit -m 'test'"
                sh "git push origin ce7d7f1e04e526a19b9fdb98d6cd86247d7844ee"
            //} else {
              //  echo "No changes detected in the repository."
            //}
        }
    }
  }
}
  post {
    success {
      echo "Pipeline succeeded"
    }
    failure {
      echo "Pipeline failed"
    }
  }
}
