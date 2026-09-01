pipeline {
    agent {
        node {
            label 'linux && java11 || java17 || java21'
        }
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building 1...'
                echo 'Building 2...'
                sleep 3
                echo 'Building 3...'
            }
        }

        stage('Test') {
            steps {
                echo 'Testing 1...'
                echo 'Testing 2...'
                sleep 3
                echo 'Testing 3...'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying 1...'
                echo 'Deploying 2...'
                sleep 3
                echo 'Deploying 3...'
            }
        }

        stage('Release') {
            steps {
                echo 'Releasing 1...'
                echo 'Releasing 2...'
                sleep 3
                echo 'Releasing 3...'
            }
        }
        
        stage('Cleanup') {
            steps {
                echo 'Cleaning up 1...'
                echo 'Cleaning up 2...'
                sleep 3
                echo 'Cleaning up 3...'
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