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
/*
        stage('Test the project') {
            steps {
                sh '''
                . venv/bin/activate
                python -m unittest
                '''
            }
        }
*/
        stage('Docker Build') {
            steps {
                sh 'docker build -t ahmedelsayad/python-app .'
            }
        }

        stage('Docker Push') {
            steps {
                withDockerRegistry([credentialsId: 'docker-hub-creds', url: '']) {
                    sh 'docker push ahmedelsayad/python-app'
                }
            }
        }
    }
}
