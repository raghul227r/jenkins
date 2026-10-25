
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
                echo "Code checked out successfully"
            }
        }

        stage('Build') {
            steps {
                sh '''
                    echo "Building application..."
                    chmod +x app.sh
                    nohup ./app.sh &
                '''
            }
        }

        stage('Test') {
            steps {
                sh '''
                    echo "Running tests..."
                    test -f app.sh
                    echo "Test passed"
                '''
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully'
            emailext(
                to: 'raghul.amadon@gmail.com',
                subject: "Build Successful: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: """Build completed successfully.

Job: ${env.JOB_NAME}
Branch: ${env.BRANCH_NAME}
Build Number: ${env.BUILD_NUMBER}
Build URL: ${env.BUILD_URL}"""
            )
        }
        failure {
            echo 'Pipeline failed'
            emailext(
                to: 'raghul.amadon@gmail.com',
                subject: "Build failed: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                body: """Build failed successfully.

Job: ${env.JOB_NAME}
Branch: ${env.BRANCH_NAME}
Build Number: ${env.BUILD_NUMBER}
Build URL: ${env.BUILD_URL}"""
            )
                
        }
    }
}
