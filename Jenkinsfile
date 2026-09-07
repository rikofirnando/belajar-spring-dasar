pipeline {
    /*
     * Tidak ada Agent global.
     * Setiap stage menentukan Agent masing-masing.
     */
    agent none

    environment {
        JAVA_HOME = '/usr/lib/jvm/java-11-openjdk-amd64'
        PATH+JAVA = '/usr/lib/jvm/java-11-openjdk-amd64/bin'
    }

    options {
        timestamps()
        timeout(time: 30, unit: 'MINUTES')
        disableConcurrentBuilds()
        buildDiscarder(logRotator(numToKeepStr: '10'))
    }

    stages {
        stage('Check Java') {
            agent {
                label 'jenkins-agent-01'
            }

            steps {
                script {
                    echo "Start Job: ${env.JOB_NAME}"
                    echo "Build Number: ${env.BUILD_NUMBER}"
                    echo "Branch Name: ${env.BRANCH_NAME}"
                    echo "--------------------------------"
                    echo "Node Jenkins : ${env.NODE_NAME}"
                    echo "Label Node   : ${env.NODE_LABELS}"
                    echo "Workspace    : ${pwd()}"
                    echo "/bin/sh tersedia : ${fileExists('/bin/sh')}"
                    echo "mvnw tersedia    : ${fileExists('mvnw')}"
                    echo "pom.xml tersedia : ${fileExists('pom.xml')}"
                }

                timeout(time: 5, unit: 'MINUTES') {
                    sh(
                        label: 'Check Agent, Java and Maven',
                        script: '''
                            set -eux

                            echo "===== INFORMASI AGENT ====="
                            echo "User      : $(whoami)"
                            echo "Hostname  : $(hostname)"
                            echo "Workspace : $(pwd)"
                            echo "Shell     : $(command -v sh)"
                            echo "Nohup     : $(command -v nohup)"

                            echo "===== WORKSPACE ====="
                            ls -ld .
                            df -h .
                            findmnt -T "$(pwd)" || true

                            echo "===== JAVA ====="
                            echo "JAVA_HOME=$JAVA_HOME"
                            echo "PATH=$PATH"
                            java -version

                            echo "===== MAVEN WRAPPER ====="
                            test -f mvnw
                            chmod +x mvnw
                            ./mvnw --version
                        '''
                    )
                }
            }
        }

        stage('Clean') {
            agent {
                label 'jenkins-agent-01'
            }

            steps {
                script {
                    echo "Clean berjalan pada node: ${env.NODE_NAME}"
                    echo "Workspace: ${pwd()}"

                    for (int i = 1; i <= 5; i++) {
                        echo "Cleaning up... ${i}/5"
                        sleep(time: 1, unit: 'SECONDS')
                    }
                }

                timeout(time: 10, unit: 'MINUTES') {
                    sh(
                        label: 'Maven Clean',
                        script: '''
                            set -eux

                            chmod +x mvnw

                            ./mvnw \
                                --batch-mode \
                                --no-transfer-progress \
                                clean
                        '''
                    )
                }
            }
        }

        stage('Test') {
            agent {
                label 'jenkins-agent-01'
            }

            steps {
                script {
                    echo "Test berjalan pada node: ${env.NODE_NAME}"
                    echo "Workspace: ${pwd()}"

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

                    echo 'File data.json berhasil dibuat'
                }

                timeout(time: 15, unit: 'MINUTES') {
                    sh(
                        label: 'Maven Test',
                        script: '''
                            set -eux

                            chmod +x mvnw

                            echo "Maven test dimulai"

                            ./mvnw \
                                --batch-mode \
                                --no-transfer-progress \
                                test

                            echo "Maven test selesai"
                        '''
                    )
                }
            }

            post {
                always {
                    junit(
                        testResults: '**/target/surefire-reports/*.xml',
                        allowEmptyResults: true
                    )

                    archiveArtifacts(
                        artifacts: 'data.json, **/target/surefire-reports/**',
                        allowEmptyArchive: true,
                        fingerprint: true
                    )
                }
            }
        }

        stage('Deploy') {
            agent {
                label 'jenkins-agent-01'
            }

            steps {
                echo "Deploy berjalan pada node: ${env.NODE_NAME}"
                echo "Workspace: ${pwd()}"

                echo 'Start deploying...'
                sleep(time: 2, unit: 'SECONDS')
                echo 'Deploy completed...'
            }
        }

        stage('Release') {
            agent {
                label 'jenkins-agent-01'
            }

            steps {
                echo "Release berjalan pada node: ${env.NODE_NAME}"
                echo "Workspace: ${pwd()}"

                echo 'Start releasing...'
                sleep(time: 2, unit: 'SECONDS')
                echo 'Release completed...'
            }
        }

        stage('Cleanup') {
            agent {
                label 'jenkins-agent-01'
            }

            steps {
                echo "Cleanup berjalan pada node: ${env.NODE_NAME}"
                echo "Workspace: ${pwd()}"

                echo 'Cleaning up 1...'
                echo 'Cleaning up 2...'
            }
        }
    }

    /*
     * Karena Pipeline menggunakan agent none, bagian post global
     * tidak mempunyai node/workspace secara otomatis.
     *
     * Jadi gunakan post global hanya untuk langkah yang tidak
     * membutuhkan workspace, seperti echo.
     */
    post {
        always {
            echo 'This will always run'
            echo "Status akhir: ${currentBuild.currentResult}"
        }

        success {
            echo 'Pipeline berhasil'
        }

        unstable {
            echo 'Pipeline berstatus UNSTABLE'
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