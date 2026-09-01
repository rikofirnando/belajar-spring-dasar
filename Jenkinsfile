pipeline {
    agent none

    stages {
        stage('Clean') {
            agent {
                label 'linux && (java11 || java17 || java21)'
            }

            steps {
                script {
                    for (int i = 0; i < 5; i++) {
                        echo "Cleaning up... ${i + 1}"
                        sleep 1
                    }
                }

                echo 'Start cleaning...'
                sh 'chmod +x mvnw'
                sh './mvnw clean'
                echo 'Finish cleaning...'
                echo 'Clean completed...'
                sleep 2
            }
        }

        stage('Test') {

            steps {
                script {
                    def data = [
                        firstName: 'John',
                        lastName : 'Doe',
                        age      : 30
                    ]

                    writeFile(
                        file: 'data.json',
                        text: groovy.json.JsonOutput.toJson(data)
                    )

                    echo 'data.json berhasil dibuat'
                }

                echo 'Start testing...'
                sh './mvnw test'
                echo 'Finish testing...'
                echo 'Test completed...'
                sleep 2
            }
        }

        stage('Deploy') {
            agent {
                label 'linux && (java11 || java17 || java21)'
            }

            steps {
                echo 'Start deploying...'
                sleep 2
                echo 'Finish deploying...'
                echo 'Deploy completed...'
            }
        }

        stage('Release') {

            steps {
                echo 'Start releasing...'
                sleep 2
                echo 'Finish releasing...'
                echo 'Release completed...'
            }
        }

        stage('Cleanup') {
            agent {
                label 'linux && (java11 || java17 || java21)'
            }

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
        }

        cleanup {
            echo 'This will always run, even if the Pipeline was aborted'
        }
    }
}