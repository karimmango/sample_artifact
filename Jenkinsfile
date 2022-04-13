pipeline {
    agent any
    tools {
       go 'go-1.17.8'
    }
    stages {
        stage('Build') {
            steps {
                sh 'go build -o sample main.go'
            }
        }
    }
//121233testing the pipeline
    post {
        always {
            archiveArtifacts artifacts: 'sample', followSymlinks: false
        }
    }
}
