
pipeline {
    
    options {
    buildDiscarder(logRotator(numToKeepStr: '20'))
    disableConcurrentBuilds()
    timeout (time: 60, unit: 'MINUTES')
    timestamps()
  }
    agent any
    
    stages {
    
        stage('Setup parameters') {
            steps {
                script {
                    properties([
                        parameters([
                        
                        choice(
                            choices: ['Dev', 'QA', 'Preprod', 'Prod'], 
                            name: 'Environment'
                                 
                                ),
                          string(
                            defaultValue: 'develop',
                            name: 'Area',
			    description: 'Enter the image Tag to deploy',
                            trim: true
                            ),
				string(
                            defaultValue: 'develop',
                            name: 'Area',
			    description: 'Enter the image Tag to deploy',
                            trim: true)
                        ])
                    ])
                }
            }
        }
        stage('Hello') {
            steps {
                sh '''
                ls -la
                pwd
                touch text.txt
                '''
            }
        }
    }
}
