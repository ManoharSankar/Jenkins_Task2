pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
                git url:'https://github.com/ManoharSankar/Jenkins_Task2.git',branch: 'main'
            }
        }
        stage('Build') {
            steps {
                sh './script.sh'
            }
        }
    }

    post {
        success {
            script {
                currentBuild.result = 'SUCCESS'
            }
            emailext(
                to: 'manoharsankar93@gmail.com',
                subject: "Jenkins Build SUCCESS: ${currentBuild.fullDisplayName}",
                body: """
                The build was successful!

                - **Build Number**: ${env.BUILD_NUMBER}
                - **Build Status**: ${currentBuild.result}
                - **Job Name**: ${env.JOB_NAME}
                - **Build URL**: ${env.BUILD_URL}

                Please check the details in Jenkins.
                """
		attachLog: true
            )
        }
        failure {
            script {
                currentBuild.result = 'FAILURE'
            }
            emailext(
                to: 'manoharsankar93@gmail.com',
                subject: "Jenkins Build FAILURE: ${currentBuild.fullDisplayName}",
                body: """
                The build failed.

                - **Build Number**: ${env.BUILD_NUMBER}
                - **Build Status**: ${currentBuild.result}
                - **Job Name**: ${env.JOB_NAME}
                - **Build URL**: ${env.BUILD_URL}

                Please check the details in Jenkins.
                """
		attachLog: true
            )
        }
    }
}
