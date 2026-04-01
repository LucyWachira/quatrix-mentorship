pipeline {
    agent any

    environment {
        INITIALS = "LW"
        SSH_KEY_ID = "traccar-ssh-key"
        REMOTE_TARGET = "lwachira@test.traccar.quatrixglobal.com"
    }

    stages {
        stage('Processing Build') {
            steps {
                echo "Running build for branch: ${env.BRANCH_NAME}"
            }
        }
        stage('Generate Remote Report') {
            steps {
                sshagent(['traccar-ssh-key']) {
                    sh """
                    ssh -o StrictHostKeyChecking=no ${env.REMOTE_TARGET} << 'EOF'
                        # 1. Generate timestamp and filename
                        NOW=\$(date +%Y%m%d-%H%M%S)
                        FILE="/tmp/${env.INITIALS}-\$NOW.txt"

                        # 2. Collect server data
                        STIME=\$(date +"%Y-%m-%d %H:%M hrs")
                        SVER=\$(lsb_release -ds)
                        SKERN=\$(uname -sr)

                        # 3. Create the report file
                        echo "Branch: ${env.BRANCH_NAME}" > "\$FILE"
                        echo "Status: ${currentBuild.currentResult}" >> "\$FILE" >> "\$FILE"
                        echo "Time: \$STIME" >> "\$FILE"
                        echo "Server Version: \$SVER" >> "\$FILE"
                        echo "Server Kernel: \$SKERN" >> "\$FILE"

                        echo "Report successfully created: \$FILE"
EOF
                    """
                }
            }
        }
    }

    post {
        success {
            script {
                githubNotify context: 'CI/CD Pipeline', description: 'Build succeeded', status: 'SUCCESS'
            }
        }
        failure {
            script {
                githubNotify context: 'CI/CD Pipeline', description: 'Build failed', status: 'FAILURE'
            }
        }
    }
}
