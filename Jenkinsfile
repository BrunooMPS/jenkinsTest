pipeline {
    agent any
    parameters {
        booleanParam(defaultValue: false, description: 'Run the second script', name: 'RUN_SECOND_SCRIPT')
    }
    stages {
        stage('Hello') {
            steps {
                script {
                    echo "${params.RUN_SECOND_SCRIPT}"
                    if (params.RUN_SECOND_SCRIPT) {
                        sh "chmod +x script1.sh && ./script2.sh"
                    }
                }
            }
        }
    }
}
