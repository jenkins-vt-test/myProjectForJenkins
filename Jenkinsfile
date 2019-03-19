pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                echo env.GIT_BRANCH
                echo env.GIT_REPO_URL
                echo env.WORKSPACE
                sh '''
                    branchPath=$(basename $env.WORKSPACE)
                    echo '$branchPath'
                    cd $branchPath
                    mkdir build
                    cd build
                    cmake ../
                    make
                '''
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
