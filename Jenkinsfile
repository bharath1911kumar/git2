pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo "Building project (static HTML site)..."
                sh 'ls -l'   // lists files to confirm checkout
            }
        }

        stage('Test') {
            steps {
                echo "Running HTML validation..."
                // Example: using tidy to validate HTML
                sh '''
                if command -v tidy >/dev/null 2>&1; then
                    tidy -errors *.html || true
                else
                    echo "tidy not installed, skipping HTML validation"
                fi
                '''
            }
        }

        stage('Deploy') {
            steps {
                echo "Deploying to web server..."
                // Example: copy files to Apache web root
                sh '''
                sudo cp -r * /var/www/html/
                sudo systemctl restart apache2
                '''
            }
        }
    }

    post {
        success {
            echo "Pipeline finished successfully ✅"
        }
        failure {
            echo "Pipeline failed ❌"
        }
    }
}
