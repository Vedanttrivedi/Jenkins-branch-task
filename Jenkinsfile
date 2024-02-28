pipeline {
    agent any

    parameters {
        choice(name: 'BRANCH', choices: '', description: 'Select branch')
    }

    stages {
        stage('Prepare') {
            steps {
                script {
                    // Discover branches and update parameter choices
                    def branches = []
                    def scmVars = checkout scm
                    for (int i = 0; i < scmVars.GIT_BRANCH.tokenize('/').size(); i++) {
                        branches.add(scmVars.GIT_BRANCH.tokenize('/')[i])
                    }
                    params.BRANCH = branches.join('\n')
                }
            }
        }
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
