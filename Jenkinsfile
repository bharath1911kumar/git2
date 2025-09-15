pipeline {
    agent { label 'Slave' }

    parameters {
        booleanParam(name: 'SKIP_TEST', defaultValue: false, description: 'Skip the test stage')
    }

    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
            }
        }

        stage('Build') {
            steps {
                echo 'Build Stage'
            }
        }

        stage('Test') {
            when {
                expression { return !params.SKIP_TEST }
            }
            steps {
                echo 'Test Stage'
            }
        }

        stage('Staging') {
            steps {
                echo 'Staging Stage'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploy Stage'
            }
        }

        stage('Post Deploy') {
            steps {
                echo 'Post Deployment Stage'
            }
        }

        stage('Prod') {
            steps {
                echo 'Prod Stage'
            }
        }
    }

    post {
        always {
            echo "Build finished"
        }
        success {
            echo "Build completed successfully!"
        }
        failure {
            echo "Build failed!"
        }
    }
}
