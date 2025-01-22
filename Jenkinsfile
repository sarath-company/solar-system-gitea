pipeline {
    agent any

    stages {
        stage('Install Dependencies') {
            steps {
                sh '''
                    npm install --no-audit
                '''
            }
        }

        stage('NPM Dependency Audit') {
            steps {
                sh '''
                    npm audit --audit-level=critical
                    echo $?
                '''
            }
        }
    }
}
