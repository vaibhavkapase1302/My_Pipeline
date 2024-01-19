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
    }```

```groovy // Stage 1: Clone the Code
        stage("Clone the Code") {
            steps {
                // Define the credentials for Git
                withCredentials([usernamePassword(credentialsId: 'gitHub', passwordVariable: 'githubPass', usernameVariable: 'githubUser')]) {
                    // Use Git to clone the repository from GitHub
                    bat "git clone https://github.com/vaibhavkapase1302/jenkins-pipeline.git -b main"
                }
            }
        }```
