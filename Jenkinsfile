pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                script {
                    def skipSecondScript = true
                        sh script1.sh
                    
                    if (skipSecondScript == true) {
                        sh script2.sh
                    }
                }
            }
        }
    }
}
