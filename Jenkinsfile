pipeline {
    agent any

    stages {
        stage('Build the project') {
            steps {
                sh 'pip install -r requirements.txt'
            }
        }

        stage('Test the project') {
            steps {
                sh 'python main.py'
            }
        }

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
}
