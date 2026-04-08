pipeline {
    agent any

    environment {
        INITIALS = "LW"
        SSH_KEY_ID = "traccar-ssh-key"
        REMOTE_TARGET = "lwachira@test.traccar.quatrixglobal.com"
        TEAMS_WEBHOOK = "https://defaulta96a137b5bac4d288f5b9ded43babd.cf.environment.api.powerplatform.com:443/powerautomate/automations/direct/workflows/4e28ac8533db4fcba263aaed71fd22f5/triggers/manual/paths/invoke?api-version=1&sp=%2Ftriggers%2Fmanual%2Frun&sv=1.0&sig=a_bFkAFbC5crTPeUkhromBCe5PWf-NqStrcOlY58xws"
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
            // Teams Notification
            office365ConnectorSend status: 'Success',
            message: "✅ Jenkins Build Successful",
            webhookUrl:"${env.TEAMS_WEBHOOK}"
            
            }
        }
        failure {
            script {
                githubNotify context: 'CI/CD Pipeline', description: 'Build failed', status: 'FAILURE'
                
             // Teams Notification
            office365ConnectorSend status: 'Failure',
             message: "❌ Jenkins Build Failed.",
            webhookUrl:"${env.TEAMS_WEBHOOK}"
            
            }
        }
    }
}
