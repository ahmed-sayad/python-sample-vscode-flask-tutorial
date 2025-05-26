@Library('sharedlib') _

pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh '''
                    python3 -m venv venv
                    . venv/bin/activate
                    pip install -r requirements.txt
                '''
            }
        }

        stage('Test') {
            steps {
                script {
                    try {
                        sh '. venv/bin/activate && python -m unittest'
                    } catch (err) {
                        echo "Tests failed"
                    }
                }
            }
        }

        stage('Docker Build & Push') {
            steps {
                script {
                    buildAndPush("ahmedelsayad/python-app:latest")
                }
            }
        }
    }
}
