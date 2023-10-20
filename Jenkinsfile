pipeline {
    agent any
    parameters {
        booleanParam(defaultValue: false, description: 'First Requirement', name: 'RUN_FIRST_REQUIREMENT')
        booleanParam(defaultValue: false, description: 'Second Requirement', name: 'RUN_SECOND_REQUIREMENT')
        booleanParam(defaultValue: false, description: 'Third Requirement', name: 'RUN_THIRD_REQUIREMENT')
        booleanParam(defaultValue: false, description: 'Run the second script', name: 'RUN_SECOND_SCRIPT')
    }
    stages {
        stage('Requirements') {
            steps {
                script {
                    def requirementParams = [
                        params.RUN_FIRST_REQUIREMENT,
                        params.RUN_SECOND_REQUIREMENT,
                        params.RUN_THIRD_REQUIREMENT,
                    ]
                    if(params.RUN_SECOND_SCRIPT == false){
                        if (requirementParams.every { it }) {
                            echo "All requirements PASSED, Push allowed on next build"
                        }else{echo "Not all Conditions met, Push NOT allowed on next build"}
                    }
                }
            }
        }
        stage('Run') {
            steps {
                script {
                    //echo "RUN_SECOND_SCRIPT: ${params.RUN_SECOND_SCRIPT}"
                    if (params.RUN_SECOND_SCRIPT) {
                        //sh "chmod +x script2.sh && ./script2.sh"
                        echo "PUSHING"
                    }
                }
            }
        }
    }
}
