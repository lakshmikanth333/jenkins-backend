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

# We are installing docker on agent cause we are going to use a docker backend file 
sudo dnf -y install dnf-plugins-core
sudo dnf config-manager --add-repo https://download.docker.com/linux/rhel/docker-ce.repo
sudo dnf install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
sudo systemctl enable --now docker
sudo systemctl start docker
sudo systemctl enable docker
sudo usermod -aG docker ec2-user 

* If you wanna push the created docker image to the ECR then install "AWS steps" plugin,
also use "withAWS(region: 'us-east-1', credentials: 'aws-creds') in pipeline. which is usefull to make comm between our jenkins and aws 



