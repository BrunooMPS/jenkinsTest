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
        //script {
          // Perform the commit and push operation here
          /*sh 'git config --global user.email "you@example.com"'
          sh 'git config --global user.name "Your Name"'
          sh 'git clone <repository_url>'
          sh 'cd <repository_directory>'
          sh 'git add .'
          sh 'git commit -m "Commit message"'
          sh 'git push origin master'*/
        //}
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