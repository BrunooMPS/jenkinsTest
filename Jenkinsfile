pipeline {
  agent any

  parameters {
    booleanParam(defaultValue: false, description: 'Run the first requirement', name: 'RUN_FIRST_REQUIREMENT')
    booleanParam(defaultValue: false, description: 'Run the second requirement', name: 'RUN_SECOND_REQUIREMENT')
    booleanParam(defaultValue: false, description: 'Run the third requirement', name: 'RUN_THIRD_REQUIREMENT')
    booleanParam(defaultValue: false, description: 'Run the second script', name: 'RUN_SECOND_SCRIPT')
  }

  stages {
    stage('checkout') {
      steps {
        script {
          checkout scm
        }
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
          runSecondScript()
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

def runSecondScript() {
  if (params.COMMIT_AND_PUSH) {
    echo "Committing and Pushing changes"
    sh "git add ."
    sh "git commit -m 'updated file'"
    sh "git push -u origin main"
  } else {
    echo "No changes to commit and push."
  }
}
