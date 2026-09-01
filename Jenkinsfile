pipeline {
    agent none

    environment {
        JAVA_HOME = '/usr/lib/jvm/java-11-openjdk-amd64'
        PATH = "/usr/lib/jvm/java-11-openjdk-amd64/bin:${env.PATH}"
    }

    stages {
        stage('Check Java') {
            agent {
                label 'jenkins-agent-01'
            }

            steps {
                sh '''
                    echo "JAVA_HOME=$JAVA_HOME"
                    echo "PATH=$PATH"
                    java -version
                    ./mvnw -version
                '''
            }
        }

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

                sh '''
                    chmod +x mvnw
                    ./mvnw clean
                '''
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
                }

                sh './mvnw test'
            }
        }

        stage('Deploy') {
            agent {
                label 'jenkins-agent-01'
            }

            steps {
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