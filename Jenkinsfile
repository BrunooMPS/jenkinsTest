pipeline {
    agent{
        label 'python'
    }
    stages {
        stage('build') {
            steps {
                script {
                    def skipSecondScript = true
                    sh "python3 script1.py"
                    
                    if (skipSecondScript == true) {
                        sh "python3 script2.py"
                    }
                }
            }
        }
    }
}