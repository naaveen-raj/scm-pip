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
archiveArtifacts artifacts: 'build/hello.txt', fingerprint:

true

sh 'echo "📦 hello.txt archived."'
}
}
}
post {
success { echo '✅ Pipeline completed successfully!' }
always { junit allowEmptyResults: true, testResults: '' }

}
}
