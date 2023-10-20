pipeline {
    agent any
    parameters {
  booleanParam 'RUN_SECOND_SCRIPT'
}
    stages {
        stage('build') {
            steps {
                script {

                    sh "chmod +x script1.sh && ./script1.sh"
                    
                    if (${params.RUN_SECOND_SCRIPT}) {
                        sh "chmod +x script2.sh && ./script2.sh"
                    }
                }
            }
        }
    }
}
