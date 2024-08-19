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
                    try {
                        sh "docker build -t todoapp:latest ."
                    } catch (Exception e) {
                        error "Docker build failed: ${e.getMessage()}"
                    }
                }
            }
        }
        stage('Docker Push') {
            steps {
                script {
                    withDockerRegistry(credentialsId: '729bbc83-fdba-45c1-93e2-9ea0344b726c') {
                        sh "docker tag todoapp:latest username/todoapp:latest"
                        sh "docker push username/todoapp:latest"
                    }
                }
            }
        }
        stage('Deploy on EC2') {
            steps {
                sshagent(['18.199.89.217']) {
                    sh """
                    ssh ec2-user@ec2-18-199-89-217.eu-central-1.compute.amazonaws.com '
                    docker stop to-do-app || true &&
                    docker rm to-do-app || true &&
                    docker pull username/todoapp:latest &&
                    docker run -d --name to-do-app -p 4000:4000 username/todoapp:latest'
                    """
                }
            }
        }
    }
}
