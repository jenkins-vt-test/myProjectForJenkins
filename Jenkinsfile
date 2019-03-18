node {
        stage 'Checkout'
                checkout scm

        stage 'Build'
                sh 'mkdir build && cd build && cmake ../'
                sh 'make'

        stage 'Test'
                sh 'make test'

}
