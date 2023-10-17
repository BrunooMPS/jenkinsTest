pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                script {
                    def skipSecondScript = true

                    sh "chmod +x script1.sh && ./script1.sh"
                    
                    if (skipSecondScript) {
                        sh "chmod +x script2.sh && ./script2.sh"
                    }
                }
            }
        }
    }
}
