pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                sh 'mkdir build'
                sh 'cd build'
                sh 'cmake ../'
                sh 'make'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
                sh 'make test'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
