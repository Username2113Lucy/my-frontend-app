stage('Update Manifest Repository') {
    steps {
        script {
            // Use withCredentials to safely access the GitHub token
            withCredentials([string(credentialsId: 'github-credentials', variable: 'GITHUB_TOKEN')]) {
                sh """
                    # Clone the repository
                    git clone https://Username2113Lucy:${GITHUB_TOKEN}@github.com/Username2113Lucy/my-frontend-manifests.git
                    cd my-frontend-manifests
                    
                    # Show current image in deployment.yaml (for debugging)
                    echo "Current image in file:"
                    grep "image:" deployment.yaml
                    
                    # Update the image tag in deployment.yaml - USING A DIFFERENT APPROACH
                    # This sed command works better on Windows
                    sed -i "s|image: baymax786/my-frontend:.*|image: baymax786/my-frontend:${DOCKER_TAG}|g" deployment.yaml
                    
                    # Also update the latest tag line if it exists
                    sed -i "s|image: baymax786/my-frontend:latest|image: baymax786/my-frontend:${DOCKER_TAG}|g" deployment.yaml
                    
                    # Show updated image (for debugging)
                    echo "Updated image in file:"
                    grep "image:" deployment.yaml
                    
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