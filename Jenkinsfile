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
    post {
        always {
            echo 'This will always run'
        }
        success {
            echo 'This will run only if successful'
        }
        failure {
            echo 'This will run only if failed'
        }
        unstable {
            echo 'This will run only if the run was marked as unstable'
        }
        changed {
            echo 'This will run only if the state of the Pipeline has changed'
            echo 'For example, if the Pipeline was previously failing but is now successful'
        }
        cleanup {
            echo 'This will always run, even if the Pipeline was aborted'
        }
    }
}