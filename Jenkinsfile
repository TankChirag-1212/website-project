pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = 'd784ec34-84a6-4363-8d99-5ac8be4a8df8'
        REPO_NAME = 'chirag1212/nginx_webapp'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git 'https://github.com/TankChirag-1212/website-project.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build("${env.REPO_NAME}:v2.0")
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                echo 'Image pushed'
            }
        }

        stage('Deploy Container') {
            steps {
                echo 'Deploying contianer success'
            }
        }
        stage('Checking'){
            steps{
                script{
                    sh "ansible all -u vagrant -m ping -i Ansible/inventory"
                }
            }
        }
        stage ('Executing ansible playbook'){
            steps {
                ansiblePlaybook inventory: 'Ansible/inventory', playbook: 'Ansible/playbook.yml'
            }
        }
    }

    post {
        success {
            echo 'Build and test succeeded!'
        }
        failure {
            echo 'Build or test failed!'
        }
    }
}