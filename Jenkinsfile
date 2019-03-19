pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                sh '''
                    rm -rf build
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
                steps {

                    sh '''
                        cd build
                        make test
                    '''
                    }
            }
        }
    }
}
