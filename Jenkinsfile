pipeline {
    agent any
    parameters {
    choice choices: ['qa', 'production','staging'], description: 'Select environment for deployment', name: 'DEPLOY_TO'
    string(name: 'upstreamJobName',
          defaultValue: 'main',
          description: 'The name of the job the triggering upstream build'
    )
  }
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
            
        steps {
            build job: 'sample', parameters: [string(name: 'DEPLOY_TO', value: 'qa'),
                                                 string(name: 'upstreamJobName', value: BRANCH_NAME)]
        }
        
        
            
        }
        stage('Run production deployment') {
          when {
            branch 'main'
          }

          steps {
            build job: 'sample', parameters: [string(name: 'DEPLOY_TO', value: 'production'),
                                                     string(name: 'upstreamJobName', value: BRANCH_NAME)]
          }
    
        

        }
    }
}
