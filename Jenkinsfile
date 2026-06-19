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
                subject: "Build SUCCESS",
                body: "Build succeeded!"
            )
        }
        failure {
            emailext (
                to: 'lavanyaramesh319@gmail.com',
                subject: "Build FAILED",
                body: "Build failed!"
            )
        }
    }
}
