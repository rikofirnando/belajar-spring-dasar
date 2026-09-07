pipeline {
    agent none

    options {
        skipDefaultCheckout(true)
        disableConcurrentBuilds()
        timeout(time: 30, unit: 'MINUTES')
    }

    environment {
        JAVA_HOME = '/usr/lib/jvm/java-11-openjdk-amd64'
        PATH = "/usr/lib/jvm/java-11-openjdk-amd64/bin:${env.PATH}"
    }

    stages {
        stage('Check Java') {
            agent {
                node {
                    label 'jenkins-agent-01'
                    customWorkspace '/home/rikofirnando/Jenkins/workspace/learn-jenkins-pipeline-scm'
                }
            }

            steps {
                checkout scm

                script {
                    echo "Start Job    : ${env.JOB_NAME}"
                    echo "Build Number: ${env.BUILD_NUMBER}"
                    echo "Node Jenkins: ${env.NODE_NAME}"
                    echo "Label Node  : ${env.NODE_LABELS}"
                    echo "Workspace   : ${pwd()}"
                    echo "mvnw ada    : ${fileExists('mvnw')}"
                    echo "pom.xml ada : ${fileExists('pom.xml')}"
                }

                timeout(time: 5, unit: 'MINUTES') {
                    sh(
                        label: 'Check Agent, Java and Maven',
                        script: '''
                            set -eux

                            echo "Agent berhasil menjalankan shell"
                            echo "JAVA_HOME=$JAVA_HOME"
                            echo "PATH=$PATH"

                            hostname
                            whoami
                            pwd

                            command -v sh
                            command -v nohup
                            command -v java

                            java -version

                            chmod +x mvnw
                            ./mvnw -version
                        '''
                    )
                }
            }
        }

        stage('Clean') {
            agent {
                node {
                    label 'jenkins-agent-01'
                    customWorkspace '/home/rikofirnando/Jenkins/workspace/learn-jenkins-pipeline-scm'
                }
            }

            steps {
                script {
                    for (int i = 0; i < 5; i++) {
                        echo "Cleaning up... ${i + 1}"
                        sleep 1
                    }
                }

                timeout(time: 10, unit: 'MINUTES') {
                    sh(
                        label: 'Maven Clean',
                        script: '''
                            set -eux
                            chmod +x mvnw
                            ./mvnw clean
                        '''
                    )
                }
            }
        }

        stage('Test') {
            agent {
                node {
                    label 'jenkins-agent-01'
                    customWorkspace '/home/rikofirnando/Jenkins/workspace/learn-jenkins-pipeline-scm'
                }
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
                        text: groovy.json.JsonOutput.prettyPrint(
                            groovy.json.JsonOutput.toJson(data)
                        )
                    )
                }

                timeout(time: 10, unit: 'MINUTES') {
                    sh(
                        label: 'Maven Test',
                        script: '''
                            set -eux
                            chmod +x mvnw
                            ./mvnw test
                        '''
                    )
                }
            }
        }

        stage('Deploy') {
            agent {
                node {
                    label 'jenkins-agent-01'
                    customWorkspace '/home/rikofirnando/Jenkins/workspace/learn-jenkins-pipeline-scm'
                }
            }

            steps {
                echo 'Start deploying...'
                sleep 2
                echo 'Deploy completed...'
            }
        }

        stage('Release') {
            agent {
                node {
                    label 'jenkins-agent-01'
                    customWorkspace '/home/rikofirnando/Jenkins/workspace/learn-jenkins-pipeline-scm'
                }
            }

            steps {
                echo 'Start releasing...'
                sleep 2
                echo 'Release completed...'
            }
        }

        stage('Cleanup') {
            agent {
                node {
                    label 'jenkins-agent-01'
                    customWorkspace '/home/rikofirnando/Jenkins/workspace/learn-jenkins-pipeline-scm'
                }
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
            echo "Status akhir: ${currentBuild.currentResult}"
        }

        success {
            echo 'Pipeline berhasil'
        }

        failure {
            echo 'Pipeline gagal'
        }

        aborted {
            echo 'Pipeline dihentikan atau mengalami timeout'
        }

        cleanup {
            echo 'Post cleanup selesai'
        }
    }
}