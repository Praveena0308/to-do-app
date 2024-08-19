pipeline {
    agent any

    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/jaiswaladi246/to-do-app.git'
            }
        }
        stage('Docker Build') {
            steps {
                script {
                    sh "docker build -t todoapp:latest ."
                }
            }
        }
        stage('Docker Push') {
            steps {
                script {
                    withDockerRegistry(credentialsId: 'your-dockerhub-credentials-id') {
                        sh "docker tag todoapp:latest username/todoapp:latest"
                        sh "docker push username/todoapp:latest"
                    }
                }
            }
        }
        stage('Deploy on EC2') {
            steps {
                sshagent(['your-ec2-ssh-credentials-id']) {
                    sh """
                    ssh ec2-user@your-ec2-public-ip 'docker pull username/todoapp:latest && docker run -d --name to-do-app -p 4000:4000 username/todoapp:latest'
                    """
                }
            }
        }
    }
}
