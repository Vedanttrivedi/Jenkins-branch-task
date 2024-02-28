pipeline {
    agent any

    parameters {
        choice(name: 'BRANCH', choices: ['v1', 'v2', 'v3', 'v4', 'v5'], description: 'Pick The branch')
    }

    stages {
        stage('Build') {
            steps {
                script {
                    // Get selected branch from parameter
                    def selectedBranch = params.BRANCH

                    // Checkout the selected branch
                    checkout([$class: 'GitSCM', branches: [[name: selectedBranch]], userRemoteConfigs: [[url: 'https://github.com/Vedanttrivedi/Jenkins-branch-task/']]])

                    // Read and display content of text file
                    def fileContent = readFile "${selectedBranch}.txt"
                    echo "Selected branch: ${selectedBranch}"
                    echo "Content of ${selectedBranch}.txt:"
                    echo "${fileContent}"
                }
            }
        }
    }
}
