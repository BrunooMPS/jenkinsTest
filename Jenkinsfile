pipeline {
    agent any

    parameters {
        booleanParam(defaultValue: false, description: 'Run the first requirement', name: 'RUN_FIRST_REQUIREMENT')
        booleanParam(defaultValue: false, description: 'Run the second requirement', name: 'RUN_SECOND_REQUIREMENT')
        booleanParam(defaultValue: false, description: 'Run the third requirement', name: 'RUN_THIRD_REQUIREMENT')
        booleanParam(defaultValue: false, description: 'Run push script', name: 'RUN_SECOND_SCRIPT')
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
                        echo "All requirements PASSED, Commit and Push allowed on the next build"
                    }
                }
            }
        }

        stage("Clone Git Repository") {
            steps {
                script {
                    if (params.RUN_SECOND_SCRIPT == true) {
                        echo "Skipping cloning, since this is a push-only script"
                    } else {
                            git(
                                url: "https://github.com/BrunooMPS/jenkinsTest.git",
                                branch: "main",
                                changelog: true,
                                poll: true,
                                credentialsId: 'YourCredentialsID'
                            )
                    }
                }
            }
        }

        stage("Create artifacts or make changes") {
            when {
                expression {
                    params.RUN_SECOND_SCRIPT == true
                }
            }
            steps {
                script {
                        sh "touch testfile"
                        sh "git add testfile"
                        sh "git commit -m 'Add testfile from Jenkins Pipeline'"
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
                    withCredentials([string(credentialsId: "testCredentials", variable: "GITHUB_PAT")]) {
                        echo "GITHUB_PAT is: ${GITHUB_PAT}"
                        sh "git push -u https://brunosusana99@hotmail.com:${GITHUB_PAT}@github.com/BrunooMPS/jenkinsTest.git main"
                    }
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
