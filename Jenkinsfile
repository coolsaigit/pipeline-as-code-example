#!groovy

// Build Parameters
properties([ parameters([
  string( name: 'nam', defaultValue: ''),
  string( name: 'AWS_ACCESS_KEY_ID', defaultValue: ''),
  string( name: 'AWS_SECRET_ACCESS_KEY', defaultValue: '')
]), pipelineTriggers([]) ])

// Environment Variables
env.AWS_ACCESS_KEY_ID = AWS_ACCESS_KEY_ID
env.AWS_SECRET_ACCESS_KEY = AWS_SECRET_ACCESS_KEY

node {
  // env.PATH += ":/opt/terraform_0.7.13/"

  stage ('Checkout') {
    checkout scm
  }

  stage ('Terraform Plan') {
    sh 'terraform init'
    sh 'terraform plan -no-color -out=create.tfplan | grep "name:" | cut -d":" -f2 | awk '{$1=$1};1' > nam' 
    println nam
  }

  // Optional wait for approval

  // stage ('Terraform Apply') {
  //   sh 'terraform apply -no-color create.tfplan'
  // }

  // stage ('Post Run Tests') {
  //   echo "Insert your infrastructure test of choice and/or application validation here."
  //   sleep 2
  //   sh 'terraform show'
  // }

  // stage ('Notification') {
  //   mail from: "saicosan@gmail.com",
  //        to: "saicosan@gmail.com",
  //        subject: "Terraform build complete",
  //        body: "Jenkins job  - build  complete"
  // }
}
