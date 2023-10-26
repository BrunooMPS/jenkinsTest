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

            // Check for changes in the repository
            //def changes = sh(returnStatus: true, script: 'git diff --exit-code')
            println(changes)
            println("hahahahahaha")
            // If there are changes, commit and push them
            //if (changes != 0) {
                sh 'git add .'
                sh "git commit -m 'test'"
                sh "git push origin main"
           // } else {
           //     echo "No changes detected in the repository."
           // }
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
