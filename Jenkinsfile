pipeline {
    agent any

    stages {
        stage('Clone repository') {
            steps {
                checkout scm
            }
        }
        
        stage('Build and push Docker image') {
            when {
                branch 'dev' // Only execute this stage if changes are on the 'dev' branch
            }
            steps {
                script {
                    def app = docker.build("tamarastojanova/devops-jenkins-exercise")
                    docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                        app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
                        app.push("${env.BRANCH_NAME}-latest")
                        // Signal the orchestrator that there is a new version
                    }
                }
            }
        }
    }
}
