pipeline {
    agent {
        node {
            label 'linux && java11 || java17 || java21'
        }
    }

    stages {
        stage('Hello') {
            steps {
                echo 'Hello world!'
            }
        }
    }
}