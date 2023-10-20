pipeline {
    agent any
    stages {
        stage('Hello') {
            steps {
                script {
                    echo "RUN_SECOND_SCRIPT: ${params.RUN_SECOND_SCRIPT}"
                    if (params.RUN_SECOND_SCRIPT) {
                        sh "chmod +x script2.sh && ./script2.sh"
                    }
                }
            }
        }
    }
}
