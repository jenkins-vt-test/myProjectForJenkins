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
                sh '''
                    cd build
                    ctest --verbose --no-compress-output -T Test || /usr/bin/true
                '''
                xunit([CTest(deleteOutputFiles: true, failIfNotNew: true, pattern: 'build/Testing/**/Test.xml', skipNoTestFiles: false, stopProcessingIfError: true)])

                script {
                  pullRequest.comment('This pullrequest is ok from step')
                }
            }
        }
    }
    post {
        success {
            script {
              pullRequest.comment('This pullrequest is ok')
            }
        }
        failure {
            script {
              pullRequest.comment('This pullrequest is not ok')
            }
        }
    }
}
