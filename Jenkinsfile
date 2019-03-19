pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                echo SCM
                echo SCM
                echo env.GIT_BRANCH
                echo env.GIT_REPO_URL
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
