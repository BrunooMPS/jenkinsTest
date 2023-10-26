pipeline {
  agent any

  parameters {
    booleanParam(defaultValue: false, description: 'Run clone script', name: 'RUN_FIRST_SCRIPT')
    booleanParam(defaultValue: false, description: 'Run the first requirement', name: 'RUN_FIRST_REQUIREMENT')
    booleanParam(defaultValue: false, description: 'Run the second requirement', name: 'RUN_SECOND_REQUIREMENT')
    booleanParam(defaultValue: false, description: 'Run the third requirement', name: 'RUN_THIRD_REQUIREMENT')
    booleanParam(defaultValue: false, description: 'Run push script', name: 'RUN_SECOND_SCRIPT')

    string(name: 'REPO_URL', defaultValue: 'https://example.git', description: 'Git repository URL')
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

    stage('Clone') {
      when{
        expression{
          params.RUN_FIRST_SCRIPT == true
        }
      }
    steps {
        script {
          sh "git clone ${params.REPO_URL}"
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
