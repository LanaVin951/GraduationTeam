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
                bat script: '
                chcp 65001
                set _workspace=C:\\WS\\GraduationWS
                set _project_name=Graduation
                set _layover_folder="C:\\GIT\\GraduationTeam\\FilesXml"
                set _db_path1="C:\\Users\\lanav\\Documents\\test1"
                set _db_path2="C:\\Users\\lanav\\Documents\\test2"
                set _db_path3="C:\\Users\\lanav\\Documents\\test3"

                md %_layover_folder%
                1cedtcli -data %_workspace% -command export --project-name %_project_name% --configuration-files %_layover_folder%

                ibcmd infobase create --db-path=%_db_path1%
                ibcmd infobase config import --db-path=%_db_path1% %_layover_folder%
                ibcmd infobase config apply -F --db-path=%_db_path1%

                ibcmd infobase config import --db-path=%_db_path2% %_layover_folder%
                ibcmd infobase config apply –F --db-path-%_db_path2%

                ibcmd infobase config import --db-path=%_db_path3% %_layover_folder%
                ibcmd infobase config apply -F --db-path=%_db_path3%
                rd /s/q %_layover_folder%
                '
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
