pipeline
{
    agent {
        label '1c-node'
    }
    environment {
        envString = 'world'
    }

    post {
        always {
            allure commandline: 'Allure 2.41.0', includeProperties: false, jdk: '', resultPolicy: 'LEAVE_AS_IS', results: [[path: 'out/syntax-check/allure']]
        }
        failure {
            bat 'echo failure'
        }
        success {
            bat 'echo succes'
        }
    }
    stages {
        stage('EDT to XML') {
            steps {
                bat 'chcp 65001\n 1cedtcli -data C:\\WS\\GraduationWS -command export --project-name Graduation --configuration-files C:\\GIT\\GraduationTeam\\FilesXml'
            }
        }
        stage('Build test base') {
            steps {
                bat 'chcp 65001\n vrunner init-dev'
            }
        }
        stage('Syntax check') {
            steps {
                bat 'chcp 65001\n vrunner syntax-check'
            }
        }
        stage('Xunit tests') {
            steps {
                    bat 'chcp 65001\n vrunner xunit'
            }
        }
    }
}
