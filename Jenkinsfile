pipeline {
    agent {
        node {
            label 'linux && java11 || java17 || java21'
        }
    }

    stages {
        stage('Clean') {
            steps {
                echo 'Start cleaning...'
                sh './mvnw clean'
                echo 'Finish cleaning...'
                echo 'Clean completed...'
                sleep 2
            }
        }

        stage('Test') {
            steps {
                echo 'Start testing...'
                sh './mvnw test'
                sh './mvnw compile test-compile'
                echo 'Finish testing...'
                echo 'Test completed...'
                sleep 2
            }
        }

        stage('Deploy') {
            steps {
                echo 'Start deploying...'
                echo 'Finish deploying...'
                echo 'Deploy completed...'
                sleep 2
            }
        }

        stage('Release') {
            steps {
                echo 'Start releasing...'
                echo 'Finish releasing...'
                echo 'Release completed...'
                sleep 2
            }
        }
        
        stage('Cleanup') {
            steps {
                echo 'Cleaning up 1...'
                echo 'Cleaning up 2...'

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