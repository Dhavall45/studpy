pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/YOUR-USERNAME/python_hello_student.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh 'docker build -t python_hello_student:latest .'
            }
        }

        stage('Stop Old Container') {
            steps {
                sh '''
                if [ $(docker ps -q -f name=student_app) ]; then
                    docker stop student_app
                    docker rm student_app
                fi
                '''
            }
        }

        stage('Run New Container') {
            steps {
                sh 'docker run -d -p 5000:5000 --name student_app python_hello_student:latest'
            }
        }

        stage('Test App') {
            steps {
                sh 'curl -I http://localhost:5000'
            }
        }
    }
}
