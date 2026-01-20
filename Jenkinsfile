pipeline {
    agent any

    stages {
        stage('Setup') {
            steps {
                echo 'Creating environment and installing dependencies'
                sh 'python3 -m venv venv'
                sh './venv/bin/pip install -r requirements.txt'
            }
        }

        stage('Verify') {
            steps {
                echo 'Running tests'
                sh './venv/bin/python3 -m unittest test_main.py'
            }
        }

        stage('Deploy') {
            when {
                expression { currentBuild.result == null || currentBuild.result == 'SUCCESS' }
            }
            steps {
                echo 'Deploying application...'
                sh 'cp main.py /tmp/deployed_app.py'
                sh 'ls -l /tmp/deployed_app.py'
            }
        }
    }
}