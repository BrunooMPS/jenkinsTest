pipeline {
  agent any

  parameters {
    booleanParam(defaultValue: false, description: 'Run the first requirement', name: 'RUN_FIRST_REQUIREMENT')
    booleanParam(defaultValue: false, description: 'Run the second requirement', name: 'RUN_SECOND_REQUIREMENT')
    booleanParam(defaultValue: false, description: 'Run the third requirement', name: 'RUN_THIRD_REQUIREMENT')
    booleanParam(defaultValue: false, description: 'Run the second script', name: 'RUN_SECOND_SCRIPT')

    string(name: 'GIT_USER_NAME', defaultValue: 'Your Name', description: 'Git user name')
    string(name: 'GIT_USER_EMAIL', defaultValue: 'you@example.com', description: 'Git user email')
    string(name: 'GIT_REPO_URL', defaultValue: 'https://example.com/your-repo.git', description: 'Git repository URL')
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
          checkRequirements()
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

def checkRequirements() {
  if (params.RUN_FIRST_REQUIREMENT && params.RUN_SECOND_REQUIREMENT && params.RUN_THIRD_REQUIREMENT) {
    echo "All requirements PASSED, Push allowed on the next build"
  }
}

def runSecondScript() {
    // Check if there are changes to commit
    def hasChanges = sh(script: 'git status --porcelain', returnStatus: true) == 0

    if (hasChanges) {
        // Perform a Git commit
        sh "git config --global user.name 'params.GIT_USER_NAME'"
        sh "git config --global user.email 'params.GIT_USER_EMAIL'"
        sh "git commit -am 'Auto-commit changes'"

        // Push changes to the remote repository
        sh "git push params.GIT_REPO_URL"
    } else {
        echo "No changes to commit or push."
    }
}