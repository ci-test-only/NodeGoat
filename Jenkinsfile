pipeline {
    agent any
    stages {
        stage('Polaris Scan') {
            steps {
                withCredentials([
                    string(credentialsId: 'polaris-prod-access-token', variable: 'POLARIS_TOKEN'),
                    string(credentialsId: 'github-token', variable: 'GITHUB_PAT')
                ]) {
                    script {
                        def status = security_scan(
                            product: 'polaris',
                            polaris_server_url: 'https://polaris.blackduck.com',
                            polaris_access_token: "${POLARIS_TOKEN}",
                            polaris_application_name: 'jenkins-training-demo',
                            polaris_project_name: 'polaris-plugin-multibranch-prcomment',
                            polaris_assessment_types: 'SAST,SCA',
                            polaris_prComment_enabled: true,
                            polaris_prComment_severities: 'CRITICAL,HIGH,MEDIUM',
                            github_token: "${GITHUB_PAT}"
                        )
                        echo "Scan status: ${status}"
                    }
                }
            }
        }
    }
}