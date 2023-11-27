pipeline {
    agent any

   environment {
    GIT_USERNAME = "${credentials('github').username}"
    GIT_PASSWORD = "${credentials('github').password}"
}

    stages {
        stage('Clone repository') {
            steps {
                checkout scm
            }
        }

        stage('Update GIT') {
            steps {
                script {
                    catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                        // Set Git configuration
                        sh "git config user.email krishnakali.dutta1177@gmail.com"
                        sh "git config user.name Krishdutta11"
                        
                        // Display content of deployment.yaml before modification
                        sh "cat deployment.yaml"
                        
                        // Update deployment.yaml with the new Docker image tag
                        sh "sed -i 's+krishdutta1177/test.*+krishdutta1177/test:${DOCKERTAG}+g' deployment.yaml"
                        
                        // Display content of deployment.yaml after modification
                        sh "cat deployment.yaml"
                        
                        // Git operations
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/kubernetesmanifest2.git HEAD:main"
                    }
                }
            }
        }
    }
}
