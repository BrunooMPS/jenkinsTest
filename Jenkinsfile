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

    stages {
    stage('Clone') {
        steps {
            script {
                // Define the Git repository URL
                def gitRepositoryURL = 'https://github.com/BrunooMPS/jenkinsTest.git' // Replace with your Git repository URL

                // Optional: Define credentials to use for authentication
                //def gitCredentials = 'your-credentials-id' // Replace with your Jenkins credentials ID

                // Optional: Set the branch to checkout
                def gitBranch = 'main' // Replace with the desired branch

                // Git clone step
                //if (gitCredentials) {
                    // Clone with credentials
                    //sh "git clone -b ${gitBranch} ${gitRepositoryURL} --credentials ${gitCredentials}"
                //} else {
                    // Clone without credentials
                    sh "git clone -b ${gitBranch} ${gitRepositoryURL}"
               // }
            }
        }
    }
    // ... other stages
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
