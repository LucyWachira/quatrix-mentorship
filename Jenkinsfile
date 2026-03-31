pipeline {
    agent any

    stages {
        stage('Trigger Build') {
            steps {
                echo "Processing branch: ${env.BRANCH_NAME}"
            }
        }
    }

    post {
        // 'always' runs regardless of success or failure to ensure the report is made
        always {
            sshagent(['traccar-ssh-key']) {
                sh """
                ssh -o StrictHostKeyChecking=no lwachira@://quatrixglobal.com << 'EOF'
                    # 1. Setup Variables on Remote Server
                    TIMESTAMP=\$(date +%Y%m%d-%H%M%S)
                    FILENAME="/tmp/LW-\${TIMESTAMP}.txt"
                    
                    # 2. Collect Data
                    S_BRANCH="${env.BRANCH_NAME}"
                    S_STATUS="${currentBuild.currentResult}"
                    S_TIME=\$(date +"%Y-%m-%d %H%M hrs")
                    S_VERSION=\$(cat /etc/os-release | grep PRETTY_NAME | cut -d'=' -f2 | tr -d '"')
                    S_KERNEL=\$(uname -sr)

                    # 3. Write to file (using a block for cleaner code)
                    {
                        echo "Branch: \$S_BRANCH"
                        echo "Status: \$S_STATUS"
                        echo "Time: \$S_TIME"
                        echo "Server Version: \$S_VERSION"
                        echo "Server Kernel: \$S_KERNEL"
                    } > \$FILENAME
                    
                    echo "Created report: \$FILENAME"
EOF
                """
            }
        }
    }
}
