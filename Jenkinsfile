stage('Update Manifest Repository') {
    steps {
        script {
            // Use withCredentials to safely access the GitHub token
            withCredentials([string(credentialsId: 'github-credentials', variable: 'GITHUB_TOKEN')]) {
                sh """
                    git clone https://Username2113Lucy:${GITHUB_TOKEN}@github.com/Username2113Lucy/my-frontend-manifests.git
                    cd my-frontend-manifests
                    
                    # Update the image tag in deployment.yaml
                    sed -i "s|image:.*|image: ${DOCKER_IMAGE}:${DOCKER_TAG}|g" deployment.yaml
                    
                    # Configure git
                    git config user.email "dharshana2113@gmail.com"
                    git config user.name "Jenkins"
                    
                    # Commit and push
                    git add deployment.yaml
                    git commit -m "Update image to version ${DOCKER_TAG}"
                    git push https://Username2113Lucy:${GITHUB_TOKEN}@github.com/Username2113Lucy/my-frontend-manifests.git main
                """
            }
        }
    }
}