pipeline {
    agent any

    stages {
        stage('Clone/Pull Repository') {
            steps {
                git branch: 'master',
                    url: 'https://github.com/227Abdulrahuman/jenkins-calculator.git'
            }
        }

        stage('Run Unit Tests') {
            steps {
                sh 'pip install unittest-xml-reporting -q'
                sh 'python -m xmlrunner discover -v --output-file test-results.xml'
            }
            post {
                always {
                    junit(
                        testResults: 'test-results.xml',
                        allowEmptyResults: true
                    )
                }
                success {
                    echo 'All tests passed successfully.'
                }
                failure {
                    echo 'Some tests failed. Check the test output above.'
                }
            }
        }
    }

    post {
        always {
            echo "Pipeline finished with status: ${currentBuild.currentResult}"
        }
    }
}
