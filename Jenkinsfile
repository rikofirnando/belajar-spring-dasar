pipeline {
    agent none

    environment {
        JAVA_HOME = '/usr/lib/jvm/java-11-openjdk-amd64'
        PATH+JAVA_HOME = '/usr/lib/jvm/java-11-openjdk-amd64/bin'
    }

    stages {
        stage('Check Java') {
            agent {
                label 'linux-java11'
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
                label 'linux-java11'
            }

            steps {
                script {
                    for (int i = 0; i < 5; i++) {
                        echo "Cleaning up... ${i + 1}"
                        sleep 1
                    }
                }

                sh '''
                    echo "Using JAVA_HOME=$JAVA_HOME"
                    chmod +x mvnw
                    ./mvnw clean
                '''
            }
        }

        stage('Test') {
            agent {
                label 'linux-java11'
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

                sh './mvnw test'
            }
        }

        stage('Deploy') {
            agent {
                label 'linux-java11'
            }

            steps {
                echo "Deploy berjalan di node: ${env.NODE_NAME}"
                echo 'Start deploying...'
                sleep 2
                echo 'Finish deploying...'
                echo 'Deploy completed...'
            }
        }

        stage('Release') {
            agent {
                label 'linux-java11'
            }

            steps {
                echo "Release berjalan di node: ${env.NODE_NAME}"
                echo 'Start releasing...'
                sleep 2
                echo 'Finish releasing...'
                echo 'Release completed...'
            }
        }

        stage('Cleanup') {
            agent {
                label 'linux-java11'
            }

            steps {
                echo "Cleanup berjalan di node: ${env.NODE_NAME}"
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