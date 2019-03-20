pipeline {
    agent any
    triggers {
       GenericTrigger(
        genericVariables: [
         [key: 'ref', value: '$.ref']
        ],
        causeString: 'Triggered on $ref',
        regexpFilterExpression: '',
        regexpFilterText: '',
        printContributedVariables: true,
        printPostContent: true
       )
    }
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
            }
        }
    }

}
