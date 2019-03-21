pipeline {
    agent any
    environment {
            repository_url = "scm.userRemoteConfigs[0].url"
    }
    stages {
        stage('build') {
            steps {
                sh '''
                    printenv
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
    post {
        success {
            script {
                env.GIT_COMMIT = sh(script: "git rev-parse HEAD", returnStdout: true).trim()
                echo env.GIT_COMMIT
                repository_name = repository_url.replace("git@github.com:","").replace(".git","")
                withCredentials([usernamePassword(credentialsId: 'd17d7c30-12bf-44d2-88f8-e9f3814e43f2', usernameVariable: 'USER', passwordVariable: 'PASSWORD')]) {
                    sh "curl -u $USER:$PASSWORD -X POST -d '{\"body\": \"Ok for the commit\"}' \"https://api.github.com/repos/${repository_name}/issues/${ghprbPullId}/comments\""
            }
         }
        }
    }
}
