pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                echo env.GIT_BRANCH
                echo env.GIT_REPO_URL
                echo '$SCM'
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
