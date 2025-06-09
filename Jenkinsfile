pipeline {
    agent { label 'agent-1' }
      environment {
        PROJECT = 'expense'
        COMPONENT = 'backend'
        appVersion = ''
      }

        options {
            disableConcurrentBuilds()
            timeout(time: 5, unit: 'MINUTES')
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
            stage('dependents') {
                steps {
                    script {
                        sh """
                        npm install
                        """
                    }
                }
            }
            stage('docker build') {
                steps {
                    script {
                        sh """
                        docker build -t backend:1.0
                        """
                    }
                }
            }
        }
        post {
            success {
                echo "pipeline succeeded"
            }
            failure {
                echo "pipeline failed"
            }
            always {
                echo "doesnt matter too me, i alwys show up"
            }
        }
}


