pipeline {
    agent any

    stages {
        stage('Build Info') {
            steps {
                echo "Running build for branch: ${env.BRANCH_NAME}"
            }
        }
    }

    post {

        success {
            sshagent(['traccar-ssh-key']) {
                sh """
                ssh -o StrictHostKeyChecking=no lwachira@test.traccar.quatrixglobal.com "
                    NOW=\$(date +%Y%m%d-%H%M%S)
                    FILE=/tmp/LW-\$NOW.txt

                    STIME=\$(date +'%Y-%m-%d %H:%M hrs')
                    SVER=\$(lsb_release -ds)
                    SKERN=\$(uname -a)

                    echo 'Branch: ${env.BRANCH_NAME}' > \$FILE
                    echo 'Status: SUCCESS' >> \$FILE
                    echo 'Time: '\$STIME >> \$FILE
                    echo 'Server Version: '\$SVER >> \$FILE
                    echo 'Server Kernel: '\$SKERN >> \$FILE
                "
                """
            }
        }

        failure {
            sshagent(['traccar-ssh-key']) {
                sh """
                ssh -o StrictHostKeyChecking=no lwachira@test.traccar.quatrixglobal.com "
                    NOW=\$(date +%Y%m%d-%H%M%S)
                    FILE=/tmp/LW-\$NOW.txt

                    STIME=\$(date +'%Y-%m-%d %H:%M hrs')
                    SVER=\$(lsb_release -ds)
                    SKERN=\$(uname -a)

                    echo 'Branch: ${env.BRANCH_NAME}' > \$FILE
                    echo 'Status: FAILED' >> \$FILE
                    echo 'Time: '\$STIME >> \$FILE
                    echo 'Server Version: '\$SVER >> \$FILE
                    echo 'Server Kernel: '\$SKERN >> \$FILE
                "
                """
            }
        }
    }
}