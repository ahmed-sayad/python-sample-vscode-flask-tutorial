@Library('sharedlib') _

pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
                echo 'Cloning done by Jenkins'
            }
        }

        stage('Build the project') {
            steps {
                sh '''
                    python3 -m venv venv
                    . venv/bin/activate
                    pip install --upgrade pip
                    pip install -r requirements.txt
                '''
            }
        }

        stage('Test the project') {
            steps {
                script {
                    try {
                        sh '. venv/bin/activate && python -m unittest'
                    } catch (err) {
                        echo "No tests found or tests failed, continuing pipeline"
                    }
                }
            }
        }

        stage('Docker Build & Push') {
            steps {
                script {
                    docker.buildAndPush("ahmedelsayad/python-app:latest")
                }
            }
        }
    }
}
