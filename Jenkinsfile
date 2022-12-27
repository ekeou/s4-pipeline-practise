pipeline {
    
    agent {
        label ("node1 || node2 || node3 || node4 || branch ||  main ||  jenkins-node || docker-agent ||  jenkins-docker2 ||  preproduction ||  production")
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
                            choices: ['DEV', 'SANDBOX', 'PROD'], 
                            name: 'Environment'
                                 
                                ),


                          string(
                            defaultValue: 's4user',
                            name: 'User',
			    description: 'Required to enter your name',
                            trim: true
                            ),

                          string(
                            defaultValue: 'v1.0.0',
                            name: 'DBTag',
			    description: 'Required to enter the image tag',
                            trim: true
                            ),

                          string(
                            defaultValue: 'v1.0.0',
                            name: 'UITag',
			    description: 'Required to enter the image tag',
                            trim: true
                            ),

                          string(
                            defaultValue: 'v1.0.0',
                            name: 'WHEATHERTag',
			    description: 'Required to enter the image tag',
                            trim: true
                            ),

                          string(
                            defaultValue: 'v1.0.0',
                            name: 'AUTHTag',
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
            when{ 
                expression {
                    env.Environment == 'DEV' }
                 }
            steps {
                sh '''
            cd UI
            docker build -t devopseasylearning2021/s4-ui:${BUILD_NUMBER}$UITag .
            cd -
            cd DB
            docker build -t devopseasylearning2021/s4-db:${BUILD_NUMBER}$DBTag .
            cd -
            cd auth 
            docker build -t devopseasylearning2021/s4-auth:${BUILD_NUMBER}$AUTHTag .
            cd -
            cd weather 
            docker build -t devopseasylearning2021/s4-weather:${BUILD_NUMBER}$WEATHERTag .
            cd -
                '''
            }
        }

        stage('Build-sandbox') {
            when{ 
                expression {
                    env.Environment == 'SANDBOX' }
                 }
            steps {
                sh '''
            cd UI
            docker build -t devopseasylearning2021/s4-ui:${BUILD_NUMBER}$UITag .
            cd -
            cd DB
            docker build -t devopseasylearning2021/s4-db:${BUILD_NUMBER}$DBTag .
            cd -
            cd auth 
            docker build -t devopseasylearning2021/s4-auth:${BUILD_NUMBER}$AUTHTag .
            cd -
            cd weather 
            docker build -t devopseasylearning2021/s4-weather:${BUILD_NUMBER}$WEATHERTag .
            cd -
                '''
            }
        }

        stage('Build-prod') {
            when{ 
                expression {
                    env.Environment == 'PROD' }
                 }
            steps {
                sh '''
            cd UI
            docker build -t devopseasylearning2021/s4-ui:${BUILD_NUMBER}$UITag .
            cd -
            cd DB
            docker build -t devopseasylearning2021/s4-db:${BUILD_NUMBER}$DBTag .
            cd -
            cd auth 
            docker build -t devopseasylearning2021/s4-auth:${BUILD_NUMBER}$AUTHTag .
            cd -
            cd weather 
            docker build -t devopseasylearning2021/s4-weather:${BUILD_NUMBER}$WEATHERTag .
            cd -
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

