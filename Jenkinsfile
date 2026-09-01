pipeline {
    agent none

    stages {
        stage('Clean') {
            agent {
                label 'jenkins-agent-01'
            }

            steps {
                script {
                    for (int i = 0; i < 5; i++) {
                        echo "Cleaning up... ${i + 1}"
                        sleep 1
                    }
                }

                echo "Running on: ${env.NODE_NAME}"
                sh 'chmod +x mvnw'
                sh './mvnw clean'
            }
        }

        stage('Test') {
            agent {
                label 'jenkins-agent-01'
            }

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

                echo "Running on: ${env.NODE_NAME}"
                sh './mvnw test'
            }
        }

        stage('Deploy') {
            agent {
                label 'jenkins-agent-01'
            }

            steps {
                echo "Deploy running on: ${env.NODE_NAME}"
                echo 'Start deploying...'
                sleep 2
                echo 'Deploy completed...'
            }
        }

        stage('Release') {
            agent {
                label 'jenkins-agent-01'
            }

            steps {
                echo "Release running on: ${env.NODE_NAME}"
                echo 'Start releasing...'
                sleep 2
                echo 'Release completed...'
            }
        }

        stage('Cleanup') {
            agent {
                label 'jenkins-agent-01'
            }

            steps {
                echo "Cleanup running on: ${env.NODE_NAME}"
                echo 'Cleaning up 1...'
                echo 'Cleaning up 2...'
            }
        }
    }

    post {
        always {
            echo "Pipeline selesai di node: ${env.NODE_NAME}"
        }

        success {
            echo 'Pipeline berhasil'
        }

        failure {
            echo 'Pipeline gagal'
        }

        cleanup {
            echo 'Post cleanup selesai'
        }
    }
}