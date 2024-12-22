pipeline {
    agent {
        kubernetes {
            // Define a simple container template for the pipeline
            containerTemplate {
                name 'shell'
                image 'ubuntu'
                command 'sleep'
                args 'infinity'
            }
            defaultContainer 'shell'
            retries 2
        }
    }
    parameters {
        // Parameter for branch selection
        choice(name: 'branchSelector', choices: ['main', 'branch1', 'branch2'], description: 'Select a branch')
    }
    stages {
        stage('Main') {
            steps {
                // Print hostname inside the container
                sh 'hostname'
            }
        }
        stage('Checkout Branch') {
            steps {
                script {
                    // Retrieve selected branch from the parameters
                    def branch = params.branchSelector
                    echo "Selected branch: ${branch}"

                    // Checkout the selected branch from the Git repository
                    checkout([
                        $class: 'GitSCM',
                        branches: [[name: "*/${branch}"]],
                        userRemoteConfigs: [[url: 'https://github.com/IdoShoshani/jenkins-parameter-choise-task-itshak.git']]
                    ])
                }
            }
        }
    }
    post {
        always {
            echo 'Pipeline completed!'
        }
    }
}
