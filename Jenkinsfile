import groovy.json.JsonOutput
//git env vars
env.git_url = 'https://manishmu@github.com/manishmu/terform.git'
env.git_branch = 'master'
env.credentials_id = '1'

//jenkins env vars
env.jenkins_server_url = 'https://10.192.8.63'
env.jenkins_node_custom_workspace_path = "/var/lib/jenkins/workspace/${JOB_NAME}"
env.jenkins_node_label = 'master'
env.terraform_version = '0.11.10'

pipeline {
agent {
node {
} 
}
stages {
stage('fetch_latest_code') {
steps {
git branch: "$git_branch" ,
credentialsId: "$credentials_id" ,
url: "$git_url"
}
}

stage('init_and_plan') {
steps {
sh "sudo terraform init $jenkins_node_custom_workspace_path"
sh "sudo terraform plan $jenkins_node_custom_workspace_path"
}
}

stage('apply_changes') {
steps {
sudo terraform apply $jenkins_node_custom_workspace_path/workspace"
}
}
}
post { 
  always { 
    cleanWs()
  }
}
