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
                script {
                    //docker.withRegistry('', DOCKERHUB_CREDENTIALS) {
                        // dockerImage.push("${env.BUILD_NUMBER}")
                    //    dockerImage.push('v2.0')
                    }
                }
            }

        stage('Deploy Container') {
            steps {
                script {
                    sh """
                    echo "deployed container"
                    // docker run -itd --name nginx-webapp-container \
                    ${env.REPO_NAME}:v2.0
                    """
                }
            }
        }
        stage ('Executing ansible playbook'){
            steps {
                ansiblePlaybook playbook: 'Ansible/playbook.yml'
            }
        }
    }

    post {
        success {
            echo 'Build and test succeeded!'
            script{
                sh """
                echo 'build successful'
                // docker rm --force nginx-webapp-container
                """
            }
        }
        failure {
            echo 'Build or test failed!'
        }
    }
}