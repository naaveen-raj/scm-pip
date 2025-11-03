pipeline {
    agent any
    options { timestamps() }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
                sh 'echo "✅ Code checkout complete."'
            }
        }
        stage('Build') {
            steps {
                sh '''
                    echo "🔨 Building the project..."
                    mkdir -p build
                    echo "Hello from Jenkins" > build/hello.txt
                '''
            }
        }
        stage('Archive') {
            steps {
                // DEBUG FIX: The 'fingerprint: true' key-value pair was
                // incorrectly split across two lines.
                // I've combined them onto one line to fix the syntax error.
                archiveArtifacts artifacts: 'build/hello.txt', fingerprint: true

                sh 'echo "📦 hello.txt archived."'
            }
        }
    }
    post {
        success { echo '✅ Pipeline completed successfully!' }
        // This block publishes test results. It's fine even if no tests
        // are found because 'allowEmptyResults: true' is set.
        always { junit allowEmptyResults: true, testResults: '' }
    }
}
