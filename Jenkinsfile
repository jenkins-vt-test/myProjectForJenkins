pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                echo env.GIT_BRANCH
                echo env.GIT_REPO_URL
                echo env.WORKSPACE
                sh '''
                    branchPath=ls | grep env.GIT_BRANCH
                    echo branchPath
                    cd branchPath
                    mkdir build
                    cd build
                    cmake ../
                    make
                '''
                }
                echo '$SCM'
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
