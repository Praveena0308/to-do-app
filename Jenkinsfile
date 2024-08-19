pipeline {
    agent any // Use any available agent (node) for this pipeline

    stages {
        stage('Checkout') {
            steps {
                // Checkout the code from the Git repository
                checkout scm
            }
        }
        
        stage('Build') {
            steps {
                // Add build steps here (e.g., compiling code)
                echo 'Building...'
                // For example, you might use:
                // sh 'mvn clean install' // for Maven projects
                // or
                // sh './build.sh' // for custom build scripts
            }
        }
        
        stage('Test') {
            steps {
                // Add testing steps here
                echo 'Testing...'
                // For example, you might use:
                // sh 'mvn test' // for Maven projects
                // or
                // sh './test.sh' // for custom test scripts
            }
        }
        
        stage('Deploy') {
            steps {
                // Add deployment steps here
                echo 'Deploying...'
                // For example, you might use:
                // sh './deploy.sh' // for custom deployment scripts
            }
        }
    }