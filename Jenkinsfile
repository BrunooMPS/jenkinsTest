pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                script {
                    def skipSecondScript = true
                    sh 'python script1.py'
                    
                    if (skipSecondScript == true) {
                        sh 'python script2.py'
                    }
                }
            }
        }
    }
}