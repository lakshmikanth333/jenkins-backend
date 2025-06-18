pipeline {
    agent { label 'agent-1'}
      environment {
        PROJECT = 'expense'
        COMPONENT = 'backend'
        appVersion = ''

      }
        stages {
            stage('Read version' ) {
                steps {
                    script {
                        def packageJson = readJSON file: 'package.json'
                        appVersion = packageJson.version
                        echo "Version is: $appVersion"
                    }

                }
            }
            stage('Installing dependencies') {
                steps {
                    script {
                        sh """

                        npm install

                        """       
                    }
                }
            }

        stage('Run Sonarqube') {
            environment {
                scannerHome = tool 'sonar-scanner-7.1';
            }
            steps {
              withSonarQubeEnv('sonar-scanner-7.1') {
                sh "${scannerHome}/bin/sonar-scanner"
                // This is generic command works for any language
              }
            }
        }

         stage('Quality Gate') {
            steps {
              timeout(time: 1, unit: 'HOURS') {
                waitForQualityGate abortPipeline: true
              }
            }
        
        }
        }
        post {
            success {
                echo "This has been succeed"
            }
            failure {
                echo "This has been failed"
            }
            
        }
}



