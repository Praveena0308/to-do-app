pipeline {
    agent any

    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Praveena0308/to-do-app.git'
            }
        }
        stage('Docker Build') {
            steps {
                script {
                    // Build Docker image with Dockerfile located in 'backend' directory
                    sh 'docker build -t todoapp:latest -f backend/Dockerfile backend'
                }
            }
        }
        stage('Docker Push') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', '0c461f4f-be61-4e7b-afd9-7a59111f2171') {
                        sh 'docker tag todoapp:latest prave987/todoapp:latest'
                        sh 'docker push prave987/todoapp:latest'

                    }
                }
            }
        }
        stage('Deploy on EC2') {
            steps {
                sshagent(['18.199.89.217']) {
                    sh """
                    ssh ec2-user@ec2-18-199-89-217.eu-central-1.compute.amazonaws.com '
                    def dockerCmd = "docker run -p 3080:3080 -d prave987/todoapp:latest"
                    sshagent(['ec2-server-key']) {
                        sh "ssh -o StrictHostKeyChecking=no ec2-user@18-199-89-217 ${dockerCmd}"

                    docker run -d --name to-do-app -p 4000:4000 username/todoapp:latest'
                    """
                }
            }
        }
    }
}
