pipeline {
    agent any
    environment {
        ARTIFACTORY_URL = "https://trialu47lau.jfrog.io/artifactory"
        ARTIFACTORY_REPO = "tf--terraform-modules-local"
        NAMESPACE = "derrickweil"
        MODULE_NAME = "your-module-name"
        VERSION = "your-version"
    }
    stages {
        stage('Install JFrog CLI') {
            steps {
                sh '''
                    if ! command -v jfrog &> /dev/null; then
                      echo "JFrog CLI not found. Installing..."
                      curl -fL https://getcli.jfrog.io | sh
                      chmod +x jfrog
                      sudo mv jfrog /usr/local/bin/ || echo "Running with local binary"
                    else
                      echo "JFrog CLI already installed."
                    fi
                '''
            }
        }
        stage('Build Artifact') {
            steps {
                // Replace with your actual build commands that generate the artifact (e.g., a .zip file).
                sh 'echo "Building artifact..."'
            }
        }
        stage('Upload Artifact') {
            steps {
                // Use the Jenkins Credentials with the ID 'artifactory-creds'
                // This credential should be of type "Username with password"
                withCredentials([usernamePassword(credentialsId: 'artifactory-creds', 
                                                  usernameVariable: 'ARTIFACTORY_USER', 
                                                  passwordVariable: 'ARTIFACTORY_API_KEY')]) {
                    sh '''
                        jfrog rt upload "dist/*.zip" "${NAMESPACE}/${MODULE_NAME}/${VERSION}/" \
                          --url="${ARTIFACTORY_URL}" --user="${ARTIFACTORY_USER}" --apikey="${ARTIFACTORY_API_KEY}"
                    '''
                }
            }
        }
    }
}
