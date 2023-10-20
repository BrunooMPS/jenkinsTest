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
                expression { params.RUN_SECOND_SCRIPT == false }
            }
            steps {
                script {
                    checkRequirements()
                }
            }
        }

        stage('Run') {
            when {
                expression { params.RUN_SECOND_SCRIPT == true }
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
    } else {
        echo "Conditions not met, Push NOT allowed on the next build"
    }
}

def runSecondScript() {
    echo "PUSHING"
}
