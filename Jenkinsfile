pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh './hello.sh'
            }
        }
    }

    post {
        success {
            emailext (
                to: 'lavanyaramesh319@gmail.com',
                subject: "Build SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: "Build succeeded!\n\n${BUILD_LOG}"
            )
        }
        failure {
            emailext (
                to: 'lavanyaramesh319@gmail.com',
                subject: "Build FAILED: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: "Build failed!\n\n${BUILD_LOG}"
            )
        }
    }
}
