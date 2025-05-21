* Install pre-requisites on master and node (jave to communicate with the master)

* install below on agent to run the buid since we are using Nodejs as the backend 
dnf module disable nodejs -y;dnf module enable nodejs:20 -y;dnf install nodejs -y

* Install "pipeline utility steps" plugin. It will let the jenkins to read the Nodejs code
The "Pipeline Utility Steps" plugin provides handy file/text operations (like reading JSON/YAML, modifying package.json, or zipping artifacts) in Jenkins pipelines.

(For Node.js, it’s great for version checks, config updates, and parsing npm outputs.) 🛠️


                    script {
                        def packageJson = readJSON file: 'package.json'
                        appVersion = packageJson.version
                        echo "Version is: $appVersion"
                    }
# above command "Reads package.json., Extracts the version field, Prints it (e.g., Version is: 1.0.0)."


