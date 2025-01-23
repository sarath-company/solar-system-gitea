pipeline {
    agent any

    stages {
        stage('Installing Dependencies') {
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

        stage('OWASP Dependency Check') {
            steps {
                dependencyCheck additionalArguments: '''
                    --scan './'
                    --out './dependency-check-report'
                    --format 'ALL'
                    --prettyPrint
                ''', odcInstallation: 'OWASP-DepCheck-10'
            }
        }
    }

    post {
        always {
            // Optionally, archive the Dependency-Check report as an artifact
            archiveArtifacts allowEmptyArchive: true, artifacts: '**/dependency-check-report/*'
        }
    }
}
