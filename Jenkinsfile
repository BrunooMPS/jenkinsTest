pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                script {
                    def skipSecondScript = true                    
                    bat "script1.bat"
                    
                    if (skipSecondScript) {
                        bat "script2.bat"
                    }
                }
            }
        }
    }
}
