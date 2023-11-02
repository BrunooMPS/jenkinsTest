pipeline {
    agent any

    parameters {
        booleanParam(defaultValue: false, description: 'Run the first requirement', name: 'RUN_FIRST_REQUIREMENT')
        booleanParam(defaultValue: false, description: 'Run the second requirement', name: 'RUN_SECOND_REQUIREMENT')
        booleanParam(defaultValue: false, description: 'Run the third requirement', name: 'RUN_THIRD_REQUIREMENT')
        booleanParam(defaultValue: false, description: 'Run push script', name: 'RUN_SECOND_SCRIPT')
    }

    stages {

        stage("Clone Repository") {
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
                        echo "All requirements PASSED, Commit and Push allowed on the next build"
                    }else{echo "NOT all requirements PASSED, Commit and Push NOT allowed on the next build"}
                }
                
            }
        }

        stage("Push to Git Repository") {
            when {
                expression {
                    params.RUN_SECOND_SCRIPT == true
                }
            }
            steps {
               script {
                //sh"git checkout main"
                sh "touch testfile"
                sh "git add ."
                sh "git commit -m 'Add testfile from Jenkins Pipeline'"
                sh "git push origin:main HEAD:origin"
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
