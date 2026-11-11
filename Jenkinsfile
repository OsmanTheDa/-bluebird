pipeline {

    agent any

    options {
        skipDefaultCheckout(true)
    }

    stages {

        stage('Checkout') {
            steps {
                echo 'Downloading Bluebird source code...'

                checkout scm

                echo 'Source code downloaded successfully.'
            }
        }

        stage('Test') {
            steps {
                echo 'Testing Bluebird website...'

                sh '''
                    if [ ! -f index.html ]; then
                        echo "ERROR: index.html is missing"
                        exit 1
                    fi

                    if ! grep -Fq "Welcome to Bluebird CI/CD!" index.html; then
                        echo "ERROR: Expected heading not found"
                        exit 1
                    fi

                    echo "SUCCESS: Bluebird website passed the tests"
                '''
            }
        }

        stage('Archive') {
            steps {
                echo 'Archiving Bluebird website...'

                archiveArtifacts artifacts: 'index.html',
                                 fingerprint: true
            }
        }
    }

    post {

        success {
            echo 'Bluebird pipeline completed successfully!'
        }

        failure {
            echo 'Bluebird pipeline failed. Check the console logs.'
        }

        always {
            echo 'Pipeline execution finished.'
        }
    }
}
