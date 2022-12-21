pipeline {
    
    agent {
        label ("node1 || node2 || node3 || node4 || branch ||  main ||  jenkins-node || docker-agent ||  jenkins-docker2 ||  preproduction ||  production")
            }
")
            }

    options {
    buildDiscarder(logRotator(numToKeepStr: '2'))
    disableConcurrentBuilds()
    timeout (time: 60, unit: 'MINUTES')
    timestamps()
  }

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
                            defaultValue: 's4user',
                            name: 'User',
			    description: 'Required to enter your name',
                            trim: true
                            ),

                          string(
                            defaultValue: 'donelogio-001',
                            name: 'DB-Tag',
			    description: 'Required to enter the image tag',
                            trim: true
                            ),

                          string(
                            defaultValue: 'donelogio-001',
                            name: 'UI-Tag',
			    description: 'Required to enter the image tag',
                            trim: true
                            ),

                          string(
                            defaultValue: 'donelogio-001',
                            name: 'WHEATHER-Tag',
			    description: 'Required to enter the image tag',
                            trim: true
                            ),

                          string(
                            defaultValue: 'donelogio-001',
                            name: 'AUTH-Tag',
			    description: 'Required to enter the image tag',
                            trim: true
                            )
                        ])
                    ])
                }
            }
        }

        stage('permission') {
            steps {
                sh '''
		cat permission.txt | grep -o $USER
		echo $?
		'''
            }
        }

        stage('Cleaning') {
            steps {
                sh '''
                ls 
                pwd
                '''
            }
        }

      
	stage('SonarQube analysis') {
            agent {
                docker {
                  image 'sonarsource/sonar-scanner-cli:4.7.0'
                }
               }
               environment {
        CI = 'true'
        //  scannerHome = tool 'Sonar'
        scannerHome='/opt/sonar-scanner'
    }
            steps{
                withSonarQubeEnv('Sonar') {
                    sh "${scannerHome}/bin/sonar-scanner"
                }
            }
        }


        stage('Build-dev') {
            steps {
                sh '''
                cd UI
docker build -t devopseasylearning2021/s4-ui:$UITag .
cd -
cd DB
docker build -t devopseasylearning2021/s4-db:$DBTag .
cd -
cd auth 
docker build -t devopseasylearning2021/s4-auth:$AUTHTag .
cd -
cd weather 
docker build -t devopseasylearning2021/s4-weather:$WEATHERTag .
cd -
                '''
            }
        }

        stage('Build-prepod') {
            steps {
                sh '''
                ls 
                pwd
                '''
            }
        }

        stage('Build-prod') {
            steps {
                sh '''
                ls 
                pwd
                '''
            }
        }

        stage('Login') {
            steps {
                sh '''
                ls 
                pwd
                '''
            }
        }

        stage('Hello') {
            steps {
                sh '''
                ls 
                pwd
                '''
            }
        }

        stage('Push-to-dockerhub-dev') {
            steps {
                sh '''
                ls 
                pwd
                '''
            }
        }

        stage('Push-to-dockerhub-preprod') {
            steps {
                sh '''
                ls 
                pwd
                '''
            }
        }

        stage('Push-to-dockerhub-prod') {
            steps {
                sh '''
                ls 
                pwd
                '''
            }
        }

        stage('Update-helm-charts-dev') {
            steps {
                sh '''
                ls 
                pwd
                '''
            }
        }

        stage('Update-helm-charts-preprod') {
            steps {
                sh '''
                ls 
                pwd
                '''
            }
        }

        stage('Update-helm-charts-prod') {
            steps {
                sh '''
                ls 
                pwd
                '''
            }
        }

        stage('Wait-for-ArgoCD') {
            steps {
                sh '''
                ls 
                pwd
                '''
            }
        }

        
    }

    post {
    
    success {
      slackSend (channel: '#development-alerts', color: 'good', message: "Images  have been pushed to Nexus")
    }

    failure {
      slackSend (channel: '#development-alerts', color: '#FF0000', message: "FAILURE: Images  have NOT been pushed to Nexus")
    }
}

}
