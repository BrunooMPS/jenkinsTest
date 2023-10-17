pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                script {
                    def skipSecondScript=false
                    echo 'Hello from false'
                    if (skipSecondScript == true) {
                        echo 'Hello from true and false'
                    }
                }
            }
        }
    }
}