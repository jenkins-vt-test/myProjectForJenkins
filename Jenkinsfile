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
                  env.GIT_COMMIT = sh(script: "git rev-parse HEAD", returnStdout: true).trim()
                  echo env.GIT_COMMIT
                  env.GIT_COMMIT.comment('This pullrequest is ok from step')
                }
            }
        }
    }
}
