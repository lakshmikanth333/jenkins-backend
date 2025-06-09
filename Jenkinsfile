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
        }
}