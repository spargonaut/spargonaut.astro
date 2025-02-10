pipeline {
    agent any

    environment {
        TARBALL_PREFIX = 'spargonaut.astro'
        REMOTE_ARCHIVE_LOCATION = "${REMOTE_ARCHIVE_ROOT}/spargonaut.astro/"
        DEV_DEPLOYMENT_LOCATION = "~/spargonaut.wtf/html"
    }

    stages {
        stage('Install Dependencies') {
            steps {
                nodejs(nodeJSInstallationName: 'v22.13.1') {
                    echo 'Installing Dependencies...'
                    sh 'npm install'
                }
            }
        }

        stage('Build Project') {
            steps {
                nodejs(nodeJSInstallationName: 'v22.13.1') {
                    echo 'Building the project...'
                    sh 'npm run build'
                }
            }
        }

        stage('Create the Archive Name') {
            steps {
                echo 'Creating the Archive Name...'
                script {
                    env.SHORT_COMMIT_HASH = sh(
                        script: 'git rev-parse --short HEAD',
                        returnStdout: true
                    ).trim()
                    echo "Short commit hash: ${env.SHORT_COMMIT_HASH}"

                    env.CURRENT_DATETIME = sh(
                        script: 'date +"%Y-%m-%d_%H-%M-%S"',
                        returnStdout: true
                    ).trim()
                    echo "Current date and time: ${env.CURRENT_DATETIME}"

                    env.ARCHIVE_NAME = "${env.TARBALL_PREFIX}_${env.CURRENT_DATETIME}_${env.SHORT_COMMIT_HASH}"
                    echo "Archive Name: ${env.ARCHIVE_NAME}.tgz"
                }
            }
        }

        stage('Compress dist directory') {
            steps {
                echo "Short commit hash before compression: ${env.SHORT_COMMIT_HASH}"
                echo 'Creating archive of dist directory...'
                sh "tar -czvf ${env.ARCHIVE_NAME}.tgz -C dist ."
            }
        }

        stage('Push tar.gz to remote server') {
            steps {
                 sshagent(credentials: ['deploy-monkey-key']) {
                    echo 'Copying tarball to remote server using SSH...'

                    sh "scp ${env.ARCHIVE_NAME}.tgz ${DEPLOYMENT_USER}@${DEPLOYMENT_SERVER}:${REMOTE_ARCHIVE_LOCATION}"
                }
            }
        }

        stage('Deploy to the dev environment') {
            steps {
                sshagent(credentials: ['deploy-monkey-key']) {
                    echo 'Copying dist files to the dev environment...'
                    sh "scp -r dist/* ${DEPLOYMENT_USER}@${DEPLOYMENT_SERVER}:${DEV_DEPLOYMENT_LOCATION}"
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished!'
        }
    }
}