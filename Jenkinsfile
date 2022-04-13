pipeline {
    agent any
    
    stages {
        stage('Build') {
            steps {
                sh 'go build -o sample main.go'
            }
        }
    }
    post {
        always {
            archiveArtifacts artifacts: 'sample', followSymlinks: false
        }
    }
}
