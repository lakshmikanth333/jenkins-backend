pipeline {
    agent { label 'agent-3'}
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
            stage('Docker build') {
                steps {
                    script {
                        sh """

                        docker build -t backend:1 .

                        """
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
