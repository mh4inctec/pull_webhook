pipeline {
    agent { label 'agent2' }

    stages {
        stage('Build') {
            steps {
                echo "Baue Projekt..."
            }
        }
    }

    post {
        always {
            script {
                configFileProvider([configFile(fileId: 'matrixSender', variable: 'MATRIX_SCRIPT')]) {
                    def matrix = evaluate(readFile(env.MATRIX_SCRIPT))
                    matrix.sendMatrixMessage(
                        'ELE',
                        "Build #${env.BUILD_NUMBER} finished with ${currentBuild.currentResult}"
                    )
                }
            }
        }
    }
}
