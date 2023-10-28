pipeline {
  agent any

  parameters {
    booleanParam(defaultValue: false, description: 'Run the first requirement', name: 'RUN_FIRST_REQUIREMENT')
    booleanParam(defaultValue: false, description: 'Run the second requirement', name: 'RUN_SECOND_REQUIREMENT')
    booleanParam(defaultValue: false, description: 'Run the third requirement', name: 'RUN_THIRD_REQUIREMENT')
    booleanParam(defaultValue: false, description: 'Run push script', name: 'RUN_SECOND_SCRIPT')
  }

  stages {
    stage('Checkout SCM') {
      steps {
        // Check out the source code from your Git repository.
        checkout scm
      }
    }

    stage('Requirements') {
      when {
        expression {
          params.RUN_SECOND_SCRIPT == false
        }
      }
      steps {
        script {
          if (params.RUN_FIRST_REQUIREMENT && params.RUN_SECOND_REQUIREMENT && params.RUN_THIRD_REQUIREMENT) {
            echo "All requirements PASSED, Commit and Push allowed on the next build"
          }
        }
      }
    }

    stage('Commit and Push') {
      when {
        expression {
          params.RUN_SECOND_SCRIPT == true
        }
      }
      steps {
        script {
          // Create a new branch to work on
          sh 'git checkout -b feature-branch'

          // Perform any necessary changes to your code here.
          // For example, you can use shell commands to modify files.

          // Commit the changes
          sh 'git add .'
          sh 'git commit -m "Automated commit"'

          // Push the changes to the Git repository
          sh 'git push origin feature-branch'
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
