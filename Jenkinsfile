pipeline {
    agent any

    environment {
        NODEJS_HOME = tool 'NodeJS 14.0.0'
        PATH = "${NODEJS_HOME}/bin:${env.PATH}"
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout code from the Git repository
                git url: 'https://github.com/Adeynike/nodejs-app.git', branch: 'main'
            }
        }

        stage('Install Dependencies') {
            steps {
                // Install Node.js dependencies
                sh 'npm install'
            }
        }

        stage('Run Tests') {
            steps {
                // Run tests using npm
                sh 'npm test'
            }
            post {
                always {
                    // Archive test results, assuming Jest is being used
                    junit '**/test-results/*.xml' // Adjust path as needed
                }
            }
        }

        stage('Build') {
            steps {
                // Build the Node.js application (if applicable)
                sh 'npm run build'
            }
        }

        stage('Deploy') {
            steps {
                // Deploy the application (e.g., copy files, run a script)
                echo 'Deploying the application...'
            }
        }
    }

    post {
        always {
            // Clean up workspace
            deleteDir()
        }
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
