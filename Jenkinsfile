pipeline {
    agent any
    tools {
        nodejs 'nodejs'  // Ensure Node.js is installed on the Jenkins agent
    }

    stages {
        stage('Git Checkout') {
            steps {
                git url: "https://github.com/Ahmedamira22/reactApp-ci-cd", branch: "main"
            }
        }

        stage('NPM Install') {
            steps {
                bat "npm install"
            }
        }
        
        stage('Node Build') {
            steps {
                bat "npm run build"
            }
        }
        
        stage('Push to GitHub') {
            steps {
                script {
                    // Configure Git user details
                    bat 'git config --global user.name "Your Name"'
                    bat 'git config --global user.email "your_email@example.com"'


                    // Check the current status of the Git workspace
                    bat 'git status'
                    
                    // Stage changes if any exist
                    bat '''
                    git add .
                    if git diff --cached --quiet; then
                    echo "No changes to commit"
                    exit 0
                    fi
                    git commit -m "Update Jenkinsfile"
                    '''

                    // Push changes to GitHub
                    bat 'git push https://github.com/Ahmedamira22/reactApp-ci-cd.git main'
                }
            }
        }
    }
}
