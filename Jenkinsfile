pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                script {
                    def skipSecondScript = true
                        Runtime.runtime.exec("script1.bat")
                    
                    if (skipSecondScript == true) {
                        Runtime.runtime.exec("script2.bat")
                    }
                }
            }
        }
    }
}
