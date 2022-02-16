pipeline {
    agent any

    stages {
        stage('Version_Check') {
            steps {
                echo 'Version Check '
                sh 'aws s3 ls'
                sh 'terraform -version'
            }
        }
        stage('Terraform_Create') {
            steps {
                echo 'Build Infra using terraform'
                checkout changelog: false, poll: false, scm: [$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/amolagudum/ec2demojenkins.git']]]
                sh 'ls'
                sh 'pwd'
                sh 'terraform init -reconfigure'
                sh 'terraform plan'
                sh 'terraform destroy -auto-approve'
                
            }
        }
    }
}
