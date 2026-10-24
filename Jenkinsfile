
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
        }
        failure {
            echo 'Pipeline failed'
        }
    }
}
