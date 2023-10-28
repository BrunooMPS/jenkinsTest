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

    stage('Make Changes in Container') {
      when {
        expression {
          params.RUN_SECOND_SCRIPT == true
        }
      }
      steps {
        script {
          // Run your container and make changes in the container's volume.
          // For example, you can use 'docker run' to start a container.

          // Copy the changes from the container's volume to the Jenkins workspace.
          sh 'docker cp container_name:/path/in/container /var/jenkins_home/workspace/testPipeline'

          // Commit and push the changes from the Jenkins workspace.
          sh 'git add .'
          sh 'git commit -m "Automated commit"'
          sh 'git push origin main'
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
