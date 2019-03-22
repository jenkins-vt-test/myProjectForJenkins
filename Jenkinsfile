pipeline {
    agent any

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
        always {
            script {
                if(env.CHANGE_ID) {
                    env.GIT_COMMIT = sh(script: "git rev-parse HEAD", returnStdout: true).trim()
                    repository_url=env.GIT_URL
                    repository_commit_id=env.CHANGE_ID
                    repository_name=repository_url.replace("https://github.com/","").replace("git@github.com:","").replace(".git","")
                    withCredentials([usernamePassword(credentialsId: 'd17d7c30-12bf-44d2-88f8-e9f3814e43f2', usernameVariable: 'USER', passwordVariable: 'PASSWORD')]) {
                        if(currentBuild.currentResult == "SUCCESS") {
                            sh "curl -u $USER:$PASSWORD -X POST -d '{\"body\": \"Jenkins approves this commit.\", \"event\": \"APPROVE\"}' \"https://api.github.com/repos/${repository_name}/pulls/${repository_commit_id}/reviews\""
                        } else {
                            sh "curl -u $USER:$PASSWORD -X POST -d '{\"body\": \"Jenkins does not approves this commit.\", \"event\": \"REQUEST_CHANGES\"}' \"https://api.github.com/repos/${repository_name}/pulls/${repository_commit_id}/reviews\""
                        }
                    }
                }
            }
        }

    }
}
