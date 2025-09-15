pipeline {
    agent any

    parameters {
        booleanParam(name: 'SKIP_TEST', defaultValue: false, description: 'Skip the Test stage?')
        booleanParam(name: 'SKIP_DEPLOY', defaultValue: false, description: 'Skip the Deploy stage?')
    }

    stages {
        stage('Build') {
            steps {
                echo "Building project (static HTML site)..."
                sh 'ls -l'
            }
        }

        stage('Test') {
            when {
                expression { return !params.SKIP_TEST }
            }
            steps {
                echo "Running HTML validation..."
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
            when {
                expression { return !params.SKIP_DEPLOY }
            }
            steps {
                echo "Deploying to web server..."
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
