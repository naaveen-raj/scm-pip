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
        
        // DEBUG FIX: The 'junit' step was failing because 'testResults: '''
        // was incorrectly matching all files (including the Jenkinsfile)
        // as test reports.
        // Since this pipeline doesn't generate XML test reports,
        // the step has been removed to fix the error.
        always {
            // The problematic line was:
            // junit allowEmptyResults: true, testResults: ''
            
            // Replaced with a simple echo. If you add tests later,
            // you can add back the junit step with a specific file pattern,
            // e.g., testResults: 'build/reports/*.xml'
            echo "Pipeline post-processing finished."
        }
    }
}

