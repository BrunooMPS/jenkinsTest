pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                script {
                    def skipSecondScript = true
                        echo "hello world"
                    
                    if (skipSecondScript == true) {
                        echo "bye world"
                    }
                }
            }
        }
    }
}
