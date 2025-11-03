pipeline {
  agent any

  parameters {
    string(name: 'FOLDER', defaultValue: '/tmp', description: 'Folder to check/create')
  }

  stages {
    stage('Check Folder') {
      steps {
        // Use single-quoted multiline so the shell expands $FOLDER at build time
        sh '''
          set -e

          TARGET="${FOLDER}"

          echo "=== Project 4: Check Folder ==="
          echo "Checking folder: ${TARGET}"

          if [ -d "${TARGET}" ]; then
            echo "Folder exists: ${TARGET}"
          else
            echo "Folder not found. Creating: ${TARGET}"
            mkdir -p "${TARGET}"
            echo "Created: ${TARGET}"
          fi

          echo "Done."
        '''
      }
    }
  }
}
