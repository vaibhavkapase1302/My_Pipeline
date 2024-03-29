# My_Pipeline

Code Checkout

```groovy
    stages {
        stage('Git Checkout') {
            steps {
                script {
                    git branch: 'main',
                        credentialsId: 'Credential ID',
                        url: 'https://github.com/username/repository.git'
                }
            }
        }
    }
```

```groovy // Stage 1: Clone the Code
        stage("Clone the Code") {
            steps {
                // Define the credentials for Git
                withCredentials([usernamePassword(credentialsId: 'gitHub', passwordVariable: 'githubPass', usernameVariable: 'githubUser')]) {
                    // Use Git to clone the repository from GitHub
                    bat "git clone https://github.com/vaibhavkapase1302/jenkins-pipeline.git -b main"
                }
            }
        }
```

Push to DockerHub

```groovy
// Stage 3: Push to Docker Hub
        stage("Push to Docker Hub") {
            steps {
                // Define the credentials for Docker Hub
                withCredentials([usernamePassword(credentialsId: 'dockerHub', passwordVariable: "dockerHubPass", usernameVariable: 'dockerHubUser')]) {
                    // Tag the Docker image with the Docker Hub repository information
                    bat "docker tag new-flask-app-v2 ${env.dockerHubUser}/new-flask-app-v2:version-v2"
                    
                    // Log in to Docker Hub using the provided credentials
                    bat "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                    
                    // Push the Docker image to Docker Hub
                    bat "docker push ${env.dockerHubUser}/new-flask-app-v2:version-v2"
                }
            }
        }
```

