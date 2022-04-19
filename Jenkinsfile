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
        stage('Save artifact') {
            steps {
              archiveArtifacts artifacts: 'sample', followSymlinks: false
                
            }
        }
        stage('run qa deploy') {
            when{
                not {
                    branch 'main'
                }
            }
            
        }
        steps {
            build job: 'sample-deploy', parameters: [string(name: 'DEPLOY_TO', value: 'production'),
                                                 string(name: 'upstreamJobName', value: BRANCH_NAME)]
        }
            
    }

}
