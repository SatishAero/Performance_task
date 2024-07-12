pipeline {
    agent any
    
    environment {
        DOCKER_REGISTRY = 'docker.io'
        DOCKER_CREDENTIALS_ID = 'dockerHubCredentials'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch:'dev',url:'https://github.com/SatishAero/Performance_task.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    def branchName = "dev"
                    def imageName = "satishvarma123/performance:${branchName}"
                    
                    docker.build(imageName, "-f Dockerfile .")
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    def branchName = "dev"
                    def containerName = "performance-${branchName}"
                    def imageName = "satishvarma123/performance:${branchName}"
                     bat "docker rm -f ${containerName} || true"
                    bat "docker run -d -p 8071:80 --name ${containerName} ${imageName}"
                }
            }
        }

       
    }

    post {
        always {
            cleanWs()
        }
    }
}
